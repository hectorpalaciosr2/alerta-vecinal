# Alerta Vecinal - Backend

Sistema de gestión de incidencias vecinales en tiempo real basado en arquitectura de microservicios.
Diseñado para manejar alto tráfico en el reporte y actualización de incidencias mediante procesamiento asíncrono y enrutamiento dinámico.

## Tech Stack

- **Lenguaje**: Java 25
- **Framework Core**: Spring Boot 4.0.6
- **Cloud/Routing**: Spring Cloud 2025.1.0 (Oakwood)
- **Persistencia**: MySQL 8+ / Spring Data JPA
- **Mensajería**: RabbitMQ
- **Seguridad**: Spring Security + JWT
- **Librerías utilitarias**: Lombok, BCrypt

*Nota técnica*: El proyecto hace uso de **Virtual Threads** (Project Loom nativo de Java) habilitados en Spring Boot 4.0 para maximizar el throughput de I/O en las llamadas entre microservicios, reemplazando el viejo modelo de hilos del SO. Para el API Gateway se utiliza `spring-cloud-starter-gateway-server-webflux` adaptado a las convenciones del release Oakwood.

## Arquitectura y Puertos

El ecosistema está compuesto por los siguientes módulos. Es crítico respetar los puertos asignados para que el API Gateway y Eureka puedan hacer el discovery correctamente de forma local.

| Servicio | Puerto Local | Descripción |
| :--- | :--- | :--- |
| **Config Server** | `8888` | Servidor centralizado de configuraciones. |
| **Eureka Server** | `8761` | Service Registry para el descubrimiento de las instancias. |
| **API Gateway** | `8080` | Punto de entrada único. Enrutamiento webflux y validación inicial JWT. |
| **Auth Service** | `8081` | Emisión y validación de tokens JWT. Registro de credenciales. |
| **Admin Service** | `8082` | Gestión CRUD de roles, estados y paramétricas. |
| **Incident Service** | `8083` | Core de negocio. Registro de incidencias y evidencias. |
| **Serenazgo Service**| `8084` | Módulo de atención, seguimiento y actualización de estados. |
| **Notification** | `8085` | Consumidor de colas RabbitMQ para el envío de alertas asíncronas. |

## Desarrollo Local

Para levantar el ecosistema en un entorno de desarrollo local (Localhost), se debe seguir estrictamente este orden de arranque para evitar timeouts de descubrimiento:

1. **Infraestructura Base**:
   Asegurarse de tener MySQL y RabbitMQ corriendo.

2. **Compilación Limpia**:
   ```bash
   mvn clean install -DskipTests -U
   ```

3. **Orden de Arranque de Microservicios**:
   - Arrancar `config-server` (esperar a que inicialice en el puerto 8888).
   - Arrancar `eureka-server` (verificar panel en `http://localhost:8761`).
   - Arrancar los microservicios de negocio (`auth`, `admin`, `incident`, `serenazgo`, `notification`).
   - Arrancar `api-gateway` al final para que pueda leer la topología completa desde Eureka.

## Variables de Entorno

Requerido setear en el IDE o en el entorno las siguientes variables antes del arranque:

- `DB_URL`: JDBC url de MySQL.
- `DB_USER` / `DB_PASSWORD`: Credenciales de base de datos.
- `JWT_SECRET`: Llave simétrica robusta para la firma de tokens.
- `RABBIT_HOST`: Host de RabbitMQ (default: localhost).
