# Docker Voting App Example

This project demonstrates Docker and Docker Compose best practices using a distributed voting application. It showcases various Docker concepts including multi-container applications, networking, volumes, and health checks.

## Docker Architecture

The application uses 5 containers, each with specific responsibilities:

- **Frontend Containers**:
  - `vote`: Python Flask app (Alpine-based)
  - `result`: Node.js app

- **Backend Containers**:
  - `redis`: In-memory queue (Alpine-based)
  - `db`: PostgreSQL database with persistent volume
  - `worker`: .NET worker service

## Docker Features Demonstrated

- **Multi-stage builds** in Vote service
- **Health checks** for Redis and PostgreSQL
- **Network segregation** with frontend/backend networks
- **Volume persistence** for PostgreSQL data
- **Container dependency** management
- **Automatic restart** policies
- **Port mapping** for web services

## Prerequisites

- Docker Engine 20.10.0+
- Docker Compose v2.0.0+
- 4GB+ RAM allocated to Docker Engine

## Docker Commands

### Starting the Application
```bash
# Build and start all services
docker compose up --build

# Run in detached mode
docker compose up -d
```

### Monitoring
```bash
# View logs
docker compose logs -f

# Check container status
docker compose ps

# Monitor container resources
docker stats
```

### Maintenance
```bash
# Stop all services
docker compose down

# Remove volumes (will delete database data)
docker compose down -v

# Rebuild specific service
docker compose build <service_name>

# Restart specific service
docker compose restart <service_name>
```

## Docker Networks

The application uses two isolated networks:
- `frontend`: For web-facing containers (vote, result)
- `backend`: For internal services (redis, db, worker)

## Volumes

- `db-data`: Persistent volume for PostgreSQL data

## Container Details

### Vote Container
- Base image: python:3.11-slim
- Multi-stage build for development and production
- Exposed port: 80
- Connected to frontend network

### Redis Container
- Alpine-based for smaller footprint
- Health check configured
- Connected to both networks for message queue

### PostgreSQL Container
- Version 9.4
- Persistent volume mounted
- Health check configured
- Connected to backend network

### Result Container
- Node.js-based web app
- Exposed port: 80
- Connected to both networks

### Worker Container
- .NET-based service
- Processes votes between Redis and PostgreSQL
- Connected to backend network only

## Development with Docker

### Rebuilding Services
If you modify any service:
```bash
docker compose build <service_name>
docker compose up -d <service_name>
```

### Viewing Logs
```bash
# All containers
docker compose logs -f

# Specific service
docker compose logs -f <service_name>
```

### Debugging
```bash
# Execute into containers
docker compose exec <service_name> sh

# View container networks
docker network ls

# Inspect container
docker compose inspect <service_name>
```