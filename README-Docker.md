# HelpDesk Docker Setup

This Docker configuration sets up a complete development environment for your Laravel + Vue.js SPA application with PostgreSQL.

## Services

- **Backend**: Laravel API (PHP 8.3.17) on port 8000
- **Frontend**: Vue.js SPA (Node 22.14) on port 3000  
- **Database**: PostgreSQL 16 on port 5432

## Quick Start

0. **Copy the example file:**
   ```bash
   cp .env.docker.example .env.docker

1. **Build and start all services:**
   ```bash
   docker-compose up --build
   ```

2. **Access the application:**
   - Frontend (Vue.js SPA): http://localhost:3000
   - Backend API: http://localhost:8000
   - Database: localhost:5432

## Database Configuration

- **Database**: helpdesk
- **Username**: helpdesk_user
- **Password**: helpdesk_password
- **Host**: postgres (internal) / localhost (external)
- **Port**: 5432

## Development Commands

**Start services in background:**
```bash
docker-compose up -d
```

**View logs:**
```bash
docker-compose logs -f [service_name]
```

**Stop services:**
```bash
docker-compose down
```

**Rebuild specific service:**
```bash
docker-compose build [service_name]
docker-compose up -d [service_name]
```

**Access container shell:**
```bash
# Backend
docker exec -it helpdesk_backend sh

# Frontend  
docker exec -it helpdesk_frontend sh

# Database
docker exec -it helpdesk_postgres psql -U helpdesk_user -d helpdesk
```

## Important Notes

- The Laravel backend automatically runs migrations on startup
- Vue.js frontend is built as a SPA and served statically
- Database data persists in Docker volumes
- CORS is configured for SPA communication between frontend and backend

## Troubleshooting

If you encounter issues:

1. **Clean rebuild:**
   ```bash
   docker-compose down -v
   docker-compose build --no-cache
   docker-compose up
   ```

2. **Check service logs:**
   ```bash
   docker-compose logs backend
   docker-compose logs frontend
   docker-compose logs postgres
   ```