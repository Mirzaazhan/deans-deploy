# DEANS Project Collaboration Guide

This guide will help you set up the DEANS project for development and collaboration.

---

## Prerequisites
- Git installed
- Docker and Docker Compose installed
- Node.js and Yarn installed

---

## Part 1: Clone the Repository and Submodules

### Step 1: Clone the Main Repository
Clone your forked `deans-deploy` repository:

```bash
git clone https://github.com/Mirzaazhan/deans-deploy.git
cd deans-deploy
```

### Step 2: Initialize and Update Submodules
The project uses three submodules (deans-api, deans-frontend, deans-notification). Initialize and populate them:

```bash
# Initialize and clone all submodules
git submodule init

# Fetch and checkout the submodules
git submodule update
```

**Alternative: Clone with Submodules in One Command**

You can also clone the repository with all submodules in a single command:

```bash
git clone --recurse-submodules https://github.com/Mirzaazhan/deans-deploy.git
cd deans-deploy
```

### Step 3: Verify Submodules
Check that all submodules are properly initialized:

```bash
git submodule status
```

You should see three submodules:
- `deans-api` → https://github.com/Mirzaazhan/deans-api
- `deans-frontend` → https://github.com/Mirzaazhan/deans-frontend
- `deans-notification` → https://github.com/Mirzaazhan/deans-notification.git

---

## Part 2: Project Setup and Deployment

### 1. Start Docker Services

#### First Time Build
Navigate to the project root (`deans-deploy`) and run:

```bash
docker-compose up --build -d
```

#### Subsequent Starts
If already built, simply run:

```bash
docker-compose up -d
```

#### Stop Services
To stop all running containers:

```bash
docker-compose down
```

---

### 2. Create and Apply Database Migrations (First Time Only)

Open a new terminal and run:

```bash
# Create migrations for the API models
docker-compose exec web python manage.py makemigrations api

# Apply all migrations to create database tables
docker-compose exec web python manage.py migrate
```

---

### 3. Create Admin Account (First Time Only)

Create a superuser account to access the Django admin panel:

```bash
docker-compose exec web python manage.py createsuperuser
```

You will be prompted to enter:
- Username
- Email address
- Password

Once created, access the admin panel at: `http://localhost/admin/`

---

### 4. Start the Frontend (React App)

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
| **Clone with Submodules** | `git clone --recurse-submodules <repo-url>` |
| **Init Submodules** | `git submodule init` |
| **Update Submodules** | `git submodule update` |
| **Pull Latest (with submodules)** | `git pull && git submodule update --remote --merge` |
| **Build & Start Docker** | `docker-compose up --build -d` |
| **Start Docker** | `docker-compose up -d` |
| **Stop Docker** | `docker-compose down` |
| **Make Migrations** | `docker-compose exec web python manage.py makemigrations api` |
| **Apply Migrations** | `docker-compose exec web python manage.py migrate` |
| **Create Admin User** | `docker-compose exec web python manage.py createsuperuser` |
| **Frontend Dev Server** | `cd deans-frontend && yarn install && yarn start` |

---

## Troubleshooting

### Submodules Not Appearing
If the submodule directories are empty after cloning:
```bash
git submodule update --init --recursive
```

### Submodule Detached HEAD
If a submodule is in "detached HEAD" state:
```bash
cd <submodule-directory>
git checkout master  # or main, depending on default branch
```

### Docker Permission Issues
On Linux/Mac, if you encounter permission issues:
```bash
sudo docker-compose up -d
```
