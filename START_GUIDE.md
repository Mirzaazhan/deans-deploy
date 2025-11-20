# DEANS Deployment Guide

## Prerequisites
- Docker and Docker Compose installed
- Node.js and Yarn installed

---

## 1. Start Docker Services

### First Time Build
Navigate to the project root (`deans-deploy`) and run:

```bash
docker-compose up --build -d
```

### Subsequent Starts
If already built, simply run:

```bash
docker-compose up -d
```

### Stop Services
To stop all running containers:

```bash
docker-compose down
```

---

## 2. Create and Apply Database Migrations (First Time Only)

Open a new terminal and run:

```bash
# Create migrations for the API models
docker-compose exec web python manage.py makemigrations api

# Apply all migrations to create database tables
docker-compose exec web python manage.py migrate
```

---

## 3. Start the Frontend (React App)

Open another new terminal and run:

```bash
# Navigate to frontend directory
cd deans-frontend

# Install dependencies (first time only)
yarn install

# Start the React development server
yarn start
```

---

## Quick Reference

| Task | Command |
|------|---------|
| **Build & Start** | `docker-compose up --build -d` |
| **Start** | `docker-compose up -d` |
| **Stop** | `docker-compose down` |
| **Migrations** | `docker-compose exec web python manage.py makemigrations api` |
| **Apply Migrations** | `docker-compose exec web python manage.py migrate` |
| **Frontend Dev Server** | `cd deans-frontend && yarn start` |