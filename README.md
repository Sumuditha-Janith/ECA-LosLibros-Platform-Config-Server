# ⚙️ LosLibros - Centralized Configuration Server

[![Java](https://img.shields.io/badge/Java-25-orange.svg)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.1.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud Config](https://img.shields.io/badge/Spring%20Cloud-Config%20Server-blue.svg)](https://spring.io/projects/spring-cloud-config)

The **Config Server** is the foundational platform component in the LosLibros microservices architecture. It provides centralized external configuration management across distributed environments for all platform modules and business services.

---

## 🌟 Features

- **Centralized Configuration Management**: Stores and serves environment configurations for all microservices in the system.
- **Hybrid Storage Support**:
  - **Git-backed**: Connected to the external configuration repository (`https://github.com/Sumuditha-Janith/ECA-LosLibros-Configurations.git`).
  - **Native Classpath Search**: Fallback local configuration files organized into `platform` and `services` folders.
- **Profile Support**: Dynamically resolves default and environment-specific profiles (e.g., `dev`, `prod`).

---

## 🏗️ Architecture & Topology

- **Service Name**: `Config-Server`
- **Default Port**: `9000`
- **Clients**: `service-registry`, `api-gateway`, `book-service`, `member-service`, `borrowing-service`

```text
Config-Server (Port 9000)
 ├── Git Remote Repository (ECA-LosLibros-Configurations)
 └── Native Classpath:
      ├── configurations/application.yaml
      ├── configurations/application-dev.yaml
      ├── configurations/platform/
      │    ├── api-gateway.yaml
      │    ├── service-registry.yaml
      │    └── service-registry-dev.yaml
      └── configurations/services/
           ├── book-service.yaml
           ├── book-service-dev.yaml
           ├── member-service.yaml
           ├── member-service-dev.yaml
           ├── borrowing-service.yaml
           └── borrowing-service-dev.yaml
```

---

## 🚀 Running the Config Server

### Prerequisites
- JDK 25 installed and configured in `JAVA_HOME`.
- Maven 3.9+ (or use the included Maven wrapper `./mvnw`).

### Launch via Maven Wrapper

```bash
cd platform/config-server
./mvnw spring-boot:run
```

### Launch via Built JAR / PM2

```bash
./mvnw clean package -DskipTests
java -jar target/Config-Server-1.0.0.jar
```

---

## 🔍 Verifying Configuration Endpoints

Once the Config Server is up on port `9000`, test the configuration endpoints using `curl` or a web browser:

```bash
# Fetch default application configuration
curl http://localhost:9000/application/default

# Fetch book-service configurations
curl http://localhost:9000/book-service/default
curl http://localhost:9000/book-service/dev

# Fetch member-service configurations
curl http://localhost:9000/member-service/default

# Fetch borrowing-service configurations
curl http://localhost:9000/borrowing-service/default

# Fetch platform gateway and registry configs
curl http://localhost:9000/api-gateway/default
curl http://localhost:9000/service-registry/default
```
