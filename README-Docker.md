# HelpDesk Docker Setup

This Docker configuration sets up a complete development environment for your Laravel + Vue.js SPA application with PostgreSQL.

## Services

- **Backend**: Laravel API (PHP 8.3.17) on port 8000  
- **Frontend**: Vue.js SPA (Node 22.14) on port 3000  
- **Database**: PostgreSQL 16 on port 5432

⚠️ **Make sure Docker Desktop is running before executing any commands.**

---

## 🚀 Quick Start

0. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/helpdesk-project.git
   cd helpdesk-project
   ```

1. **Copy the example environment file:**
   ```bash
   cp .env.docker.example .env.docker
   ```

2. **Start all services using Docker images:**
   ```bash
   docker compose --env-file .env.docker up
   ```

3. **Access the application:**
   - Frontend (Vue.js SPA): [http://localhost:3000](http://localhost:3000)
   - Backend API: [http://localhost:8000](http://localhost:8000)
   - PostgreSQL (DB): Host `localhost`, Port `5432`

---

## 🛠️ Database Configuration

- **Database**: `helpdesk`  
- **Username**: `helpdesk_user`  
- **Password**: `helpdesk_password`  
- **Host**: `postgres` (internal) / `localhost` (external)  
- **Port**: `5432`

---

## ⚙️ Development Commands

**Start services in background:**
```bash
docker compose -f docker-compose.yml --env-file .env.docker up -d
```

**View logs:**
```bash
docker compose logs -f [service_name]
```

**Stop services:**
```bash
docker compose down
```

**Rebuild specific service (only needed if modifying locally):**
```bash
docker compose build [service_name]
docker compose up -d [service_name]
```

**Access container shell:**
```bash
# Backend
docker exec -it helpdesk_backend sh

# Frontend  
docker exec -it helpdesk_frontend sh

# PostgreSQL
docker exec -it helpdesk_postgres psql -U helpdesk_user -d helpdesk
```

---

## ✅ Important Notes

- The Laravel backend automatically runs migrations on startup  
- Vue.js frontend is pre-built and served as a SPA  
- Database data persists using Docker volumes  
- CORS is configured for communication between frontend and backend  
- Make sure port 3000 and 8000 are not already in use on your system

---

## 🧰 Troubleshooting

1. **Clean rebuild (if things break):**
   ```bash
   docker compose down -v
   docker compose pull
   docker compose --env-file .env.docker up
   ```

2. **Check service logs:**
   ```bash
   docker compose logs backend
   docker compose logs frontend
   docker compose logs postgres
   ```

---

## 📂 Environment File Example (`.env.docker.example`)

```env
APP_ENV=production
APP_DEBUG=false
DB_CONNECTION=pgsql
DB_HOST=postgres
DB_PORT=5432
DB_DATABASE=helpdesk
DB_USERNAME=helpdesk_user
DB_PASSWORD=helpdesk_password
APP_URL=http://localhost:8000
FRONTEND_URL=http://localhost:3000
SANCTUM_STATEFUL_DOMAINS=localhost:3000,127.0.0.1:3000,localhost,127.0.0.1
SESSION_DOMAIN=localhost
VITE_API_URL=http://localhost:8000
```

---

Enjoy your HelpDesk app! 🎉
