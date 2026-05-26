# 🚨 Alerta Vecinal

Sistema backend basado en microservicios desarrollado con **Java Spring Boot** para la gestión de reportes ciudadanos de incidentes vecinales en tiempo real.

---

# 📌 Descripción

**Alerta Vecinal** es una plataforma backend orientada al registro y gestión de incidentes mediante una arquitectura de microservicios.

El sistema permite que los vecinos puedan reportar incidentes enviando información como:

- Tipo de incidente
- Descripción
- Dirección o referencia
- Evidencia fotográfica

Los reportes son gestionados por serenazgo, permitiendo realizar seguimiento y actualización del estado de atención de cada caso.

El proyecto está enfocado en el desarrollo de APIs REST, autenticación segura y comunicación entre microservicios utilizando Spring Boot y MySQL.

---

# 🎯 Objetivo General

Desarrollar un sistema backend basado en microservicios con Spring Boot que permita registrar y gestionar incidentes vecinales en tiempo real.

---

# ✅ Objetivos Específicos

- Implementar autenticación mediante JWT.
- Gestionar usuarios y roles.
- Registrar incidentes mediante APIs REST.
- Gestionar estados de atención.
- Aplicar arquitectura basada en microservicios.
- Persistir información utilizando MySQL.
- Implementar comunicación asíncrona mediante RabbitMQ.

---

# 🏗️ Arquitectura del Sistema

El sistema estará dividido en microservicios independientes.

## 🔐 Auth Service

Microservicio encargado de:

- Registro de usuarios
- Inicio de sesión
- Generación de JWT
- Gestión de roles
- Encriptación de contraseñas con BCrypt

---

## ⚙️ Admin Service

Microservicio encargado de:

- Gestión de usuarios
- Gestión de categorías
- Gestión de estados
- Administración general del sistema
- Consulta de estadísticas básicas

---

## 🚨 Incident Service

Microservicio encargado de:

- Registrar incidentes
- Actualizar estados
- Consultar reportes
- Historial de incidencias
- Gestión de evidencias

---

## 🛡️ Serenazgo Service

Microservicio encargado de:

- Recepción de alertas
- Visualización de incidentes
- Actualización de estados
- Seguimiento de incidentes
- Atención de reportes vecinales

---

## 🔔 Notification Service

Microservicio encargado de:

- Envío de notificaciones
- Comunicación mediante RabbitMQ
- Gestión de eventos asíncronos
- Alertas del sistema

---

# 👥 Roles del Sistema

## 👤 Vecino

Funciones:

- Registrar incidentes
- Consultar reportes
- Ver estado de atención
- Adjuntar evidencias

---

## 🛡️ Serenazgo

Funciones:

- Consultar incidentes
- Actualizar estados
- Gestionar atención de incidentes
- Dar seguimiento a reportes

### Estados disponibles

- Pendiente
- En revisión
- En camino
- Atendido
- Cerrado

---

## ⚙️ Administrador

Funciones:

- Gestionar usuarios
- Gestionar categorías
- Gestionar estados
- Visualizar estadísticas
- Administrar el sistema

---

# 🔄 Flujo del Sistema

## 1️⃣ Registro del incidente

El vecino envía:

- Tipo de incidente
- Descripción
- Dirección o referencia
- Evidencia fotográfica

---

## 2️⃣ Procesamiento

El Incident Service procesa y almacena la información en MySQL.

---

## 3️⃣ Atención del incidente

El Serenazgo Service consulta los incidentes y actualiza el estado del caso.

---

## 4️⃣ Comunicación asíncrona

El Notification Service envía eventos y alertas mediante RabbitMQ.

---

## 5️⃣ Seguimiento

El vecino consulta el estado del incidente mediante la API REST.

---

# 🛠️ Tecnologías Utilizadas

## Backend

- Java 17
- Spring Boot
- Spring Security
- Spring Data JPA

---

## Base de Datos

- MySQL

---

## Arquitectura

- Microservicios
- API REST
- JWT Authentication
- RabbitMQ

---

## Seguridad

- BCrypt Password Encoder
- JWT Authentication
- Roles y permisos

---

## Herramientas

- Maven
- Docker
- Postman
- GitHub

---

# 🗄️ Entidades Principales

- Usuarios
- Roles
- Incidentes
- Categorías
- Evidencias
- Estados
- Serenazgo
- Notificaciones

---

# 📡 Endpoints Principales

## 🔐 Auth Service

```http
POST /api/auth/login
POST /api/auth/register
```

---

## ⚙️ Admin Service

```http
GET /api/admin/users
POST /api/admin/categories
PUT /api/admin/states/{id}
```

---

## 🚨 Incident Service

```http
POST /api/incidents
GET /api/incidents
GET /api/incidents/{id}
PUT /api/incidents/{id}
```

---

## 🛡️ Serenazgo Service

```http
GET /api/serenazgo/incidents
PUT /api/serenazgo/incidents/{id}/status
```

---

# 🔐 Seguridad

El sistema implementa mecanismos de seguridad utilizando:

- JWT Authentication
- BCrypt para encriptación de contraseñas
- Control de acceso por roles
- Middleware de autorización
- Validación de endpoints

### Ejemplo BCrypt

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}
```

---

# 📂 Estructura General

```bash
alerta-vecinal/
│
├── auth-service/
├── admin-service/
├── incident-service/
├── serenazgo-service/
├── notification-service/
│
├── api-gateway/
├── eureka-server/
├── config-server/
│
├── docker-compose.yml
└── README.md
```

---

# 📊 Beneficios

- Arquitectura escalable
- Servicios independientes
- Fácil mantenimiento
- APIs reutilizables
- Mejor organización del backend
- Comunicación asíncrona entre servicios

---

# 🚀 Mejoras Futuras

- Dashboard en tiempo real
- Notificaciones push
- Integración con aplicación móvil
- Docker Compose
- Kubernetes
- Monitoreo con Spring Boot Admin

---

# 📦 Instalación

## Clonar repositorio

```bash
git clone https://github.com/usuario/alerta-vecinal.git
```

---

## Ingresar al proyecto

```bash
cd alerta-vecinal
```

---

## Ejecutar microservicios

```bash
mvn spring-boot:run
```
