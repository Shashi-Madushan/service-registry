# Service-Registry

A service discovery server built on Netflix Eureka. All microservices register themselves here on startup, allowing the API Gateway and other services to locate them dynamically by name rather than hardcoded URLs.

## About

The Service-Registry is a Netflix Eureka-based service discovery component that enables automatic registration and discovery of microservices. It maintains a registry of all running service instances and their health status, facilitating dynamic service location and load balancing across the ECA microservices ecosystem.

## Tech Stack

| Technology | Details |
|---|---|
| Java | 25 |
| Spring Boot | 4.0.3 |
| Spring Cloud | 2025.1.0 |
| Spring Cloud Netflix Eureka Server | Service discovery |
| Spring Cloud Config Client | Fetches config from Config-Server |

## How It Works

The Service-Registry acts as the central directory for the microservices architecture. When a service starts, it registers with this server. The API Gateway queries this registry to resolve service locations using load-balanced URIs (e.g., `lb://STUDENT-SERVICE`).

## Service Details

| Property | Value |
|---|---|
| Port | `9001` |
| Artifact ID | `Service-Registry` |
| Group ID | `lk.ijse.eca` |
| Config Source | `http://localhost:9000` (Config-Server) |

## Getting Started

Follow the lecture guidelines, refer to the lecture video for more information and how to get started correctly.

> **Important:** Config-Server must be running before starting the Service-Registry, as it fetches its configuration from Config-Server on startup.

**Startup order:**
1. Config-Server (`9000`)
2. **Service-Registry** (`9001`)
3. IAM-Service
4. Product-Service
5. Order-Service

```bash
./mvnw spring-boot:run
```

The Eureka dashboard will be available at: `http://localhost:9001`

## Troubleshoot

| Issue | Solution |
|---|---|
| Service fails to start | Verify Config-Server is running on port 9000 before starting Service-Registry |
| Services not registering | Check network connectivity and Eureka client configuration in service YAML files |
| Eureka dashboard not accessible | Confirm port 9001 is not in use by another process |
| Config fetch timeout | Verify `spring.cloud.config.uri` points to correct Config-Server URL |
| Services showing as DOWN | Check service health endpoints and database connectivity for domain services |
