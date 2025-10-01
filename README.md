# 🔌 PowerMate
### Sistema de Gestión de Energía para Hogares Inteligentes

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://openjdk.java.net/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![Maven](https://img.shields.io/badge/Maven-3.8+-red.svg)](https://maven.apache.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📋 Tabla de Contenidos
- [Descripción del Proyecto](#-descripción-del-proyecto)
- [Características Principales](#-características-principales)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Arquitectura del Sistema](#-arquitectura-del-sistema)
- [Instalación y Configuración](#-instalación-y-configuración)
- [API Endpoints](#-api-endpoints)
- [Testing](#-testing)
- [Equipos de Desarrollo](#-equipos-de-desarrollo)
- [Contribución](#-contribución)

## 🎯 Descripción del Proyecto

PowerMate es un sistema backend desarrollado en Spring Boot que permite a los usuarios gestionar y monitorear el consumo energético de dispositivos inteligentes en sus hogares. El sistema facilita el ahorro de energía mediante el control remoto, programación automática y alertas personalizadas.

### Objetivos Principales
- 🏠 **Gestión de Dispositivos**: Control completo de dispositivos inteligentes
- 📊 **Monitoreo en Tiempo Real**: Seguimiento del consumo energético
- ⏰ **Programación Automática**: Horarios de encendido/apagado
- 🚨 **Sistema de Alertas**: Notificaciones por umbrales de consumo
- 📈 **Reportes Históricos**: Análisis de patrones de consumo

## ✨ Características Principales

### 🔐 Autenticación y Seguridad
- Autenticación básica con Spring Security
- Encriptación de contraseñas con BCrypt
- Control de acceso por roles (ADMIN/USER)
- Configuración CORS para integración frontend

### 🏠 Gestión de Dispositivos
- CRUD completo de dispositivos inteligentes
- Asociación de dispositivos a usuarios
- Control de estado (encendido/apagado)
- Gestión de potencia y consumo

### 📊 Monitoreo de Consumo
- Registro automático de consumo energético
- Historial temporal de datos
- Cálculo de consumo por dispositivo
- Métricas en tiempo real

### ⏰ Programación Inteligente
- Configuración de horarios automáticos
- Encendido/apagado programado
- Gestión de múltiples horarios por dispositivo
- Validación de conflictos de horarios

### 🚨 Sistema de Alertas
- Configuración de umbrales personalizados
- Notificaciones por consumo excesivo
- Alertas por dispositivo específico
- Historial de alertas generadas

## 🛠 Tecnologías Utilizadas

### Backend
- **Java 21** - Lenguaje de programación
- **Spring Boot 3.4.0** - Framework principal
- **Spring Security** - Autenticación y autorización
- **Spring Data JPA** - Persistencia de datos
- **Hibernate** - ORM

### Base de Datos
- **MySQL 8.0** - Base de datos relacional
- **JPA/Hibernate** - Mapeo objeto-relacional

### Testing
- **JUnit 5** - Framework de testing
- **Mockito** - Mocking framework
- **Spring Boot Test** - Testing de integración

### Herramientas de Desarrollo
- **Maven** - Gestión de dependencias
- **Lombok** - Reducción de código boilerplate
- **Jackson** - Serialización JSON
- **MySQL Workbench** - Gestión de base de datos

## 🏗 Arquitectura del Sistema

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Controllers   │    │    Services     │    │  Repositories  │
│                 │    │                 │    │                 │
│ • UserController│◄──►│ • UserService   │◄──►│ • UserRepository│
│ • DeviceController│   │ • DeviceService │    │ • DeviceRepository│
│ • AlertsController│   │ • AlertsService │    │ • AlertRepository│
│ • ScheduleController│ │ • ScheduleService│   │ • ScheduleRepository│
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│      DTOs       │    │     Models      │    │   Database      │
│                 │    │                 │    │                 │
│ • UserDTO       │    │ • User          │    │ • users         │
│ • DeviceDTO     │    │ • Device        │    │ • devices       │
│ • AlertsDTO     │    │ • Alerts        │    │ • alerts        │
│ • ScheduleDTO   │    │ • Schedule      │    │ • schedules     │
│ • ConsRecordDTO │    │ • ConsRecord    │    │ • consumption_records│
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🚀 Instalación y Configuración

### Prerrequisitos
- Java 21 o superior
- Maven 3.8+
- MySQL 8.0
- Git

### Pasos de Instalación

1. **Clonar el repositorio**
```bash
git clone https://github.com/tu-usuario/powermate.git
cd powermate
```

2. **Configurar la base de datos**
```sql
CREATE DATABASE testdb;
```

3. **Configurar variables de entorno**
```properties
# Editar src/main/resources/application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/testdb?createDatabaseIfNotExist=true
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña
```

4. **Instalar dependencias**
```bash
mvn clean install
```

5. **Ejecutar la aplicación**
```bash
mvn spring-boot:run
```

La aplicación estará disponible en `http://localhost:8080`

## 📡 API Endpoints

### Autenticación
```
POST /api/admin/register    - Registrar nuevo usuario
```

### Usuarios
```
GET    /api/users           - Listar usuarios
PUT    /api/admin/users/{id} - Actualizar usuario
DELETE /api/admin/users/{id} - Eliminar usuario
```

### Dispositivos
```
GET    /api/devices         - Listar dispositivos
POST   /api/devices         - Crear dispositivo
GET    /api/devices/{id}    - Obtener dispositivo
PUT    /api/devices/{id}    - Actualizar dispositivo
DELETE /api/devices/{id}    - Eliminar dispositivo
PUT    /api/devices/{id}/status - Cambiar estado
```

### Consumo
```
GET    /api/consumption     - Obtener registros de consumo
POST   /api/consumption     - Registrar consumo
GET    /api/consumption/{deviceId} - Consumo por dispositivo
```

### Alertas
```
GET    /api/alerts          - Listar alertas
POST   /api/alerts          - Crear alerta
PUT    /api/alerts/{id}     - Actualizar alerta
DELETE /api/alerts/{id}     - Eliminar alerta
```

### Programación
```
GET    /api/schedules       - Listar horarios
POST   /api/schedules       - Crear horario
PUT    /api/schedules/{id}  - Actualizar horario
DELETE /api/schedules/{id}  - Eliminar horario
```

## 🧪 Testing

### Ejecutar Tests
```bash
# Ejecutar todos los tests
mvn test

# Ejecutar tests con cobertura
mvn test jacoco:report
```

### Cobertura de Testing
- **Cobertura mínima**: 60%
- **Tests unitarios**: Controllers, Services, Models
- **Frameworks**: JUnit 5, Mockito, Spring Boot Test

## 👥 Equipos de Desarrollo

### EQUIPO 1: Usuarios y Dispositivos
* **PRODUCT OWNER**: Andrés Vázquez [Github](https://github.com/andresvaz89)
* **SCRUM MASTER**: Roberto Lumbreras [Github](https://github.com/roberto-lumbreras)
* **DEVELOPERS**: 
  - Maria García [Github](https://github.com/strawmery)
  - Abel Prieto [Github](https://github.com/abelpriem)
  - Naudelyn Lucena [Github](https://github.com/NaudelynLucena)
  - Pilar Pato [Github](https://github.com/Pilar-Pato)
  - Lara Gutiérrez [Github](https://github.com/lara-gs)
  - Ana Hernández [Github](https://github.com/AnaBHernandez)
  - Susana Artime [Github](https://github.com/Susana-Artime)
  - Rubén Blanco [Github](https://github.com/Ruben-BV)

### EQUIPO 2: Consumo y Optimización
* **PRODUCT OWNER**: Acacia Sánchez Pastur [Github](https://github.com/Acacia-Sanchez)
* **SCRUM MASTER**: Juan Camilo [Github](https://github.com/Juanito2005)
* **DEVELOPERS**:
  - Adrian Caiñas [Github](https://github.com/acr00)
  - Andrea Martinez [Github](https://github.com/andreamsgi27)
  - Óscar Menéndez [Github](https://github.com/Morty1904)
  - Mercy Chancayauri [Github](https://github.com/mercyluz)
  - Alejandra Sierra [Github](https://github.com/alejandra-sierra)
  - Estefany Ochoa [Github](https://github.com/EstefanyOchoaRomero)
  - Kevin Boy [Github](https://github.com/sealkboy)
  - Guadalupe G.Figeroa [Github](https://github.com/GuadalupeGFigueroa)

## 🤝 Contribución

### Flujo de Trabajo
1. Fork del repositorio
2. Crear rama feature desde `dev`: `git checkout -b feat/SGE1-XX:descripcion`
3. Realizar cambios y commits descriptivos
4. Crear Pull Request hacia `dev`
5. Revisión y aprobación por otro miembro del equipo
6. Merge y eliminación de la rama

### Convenciones de Commits
```
feat(SGE1-XX): Agregar nueva funcionalidad
fix(SGE1-XX): Corregir bug existente
docs(SGE1-XX): Actualizar documentación
test(SGE1-XX): Agregar o modificar tests
```

### Estándares de Código
- Cobertura de testing mínima: 60%
- Uso de Postman para testing de endpoints
- Documentación actualizada en cada PR
- Código limpio y comentarios descriptivos

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

## 📞 Contacto

Para preguntas o sugerencias sobre el proyecto, contacta con el equipo de desarrollo a través de los enlaces de GitHub proporcionados arriba.

---

**Desarrollado con ❤️ por los equipos de Factoria F5**
