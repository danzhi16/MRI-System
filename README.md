# MRI Analysis System

Professional full-stack MRI analysis platform with:
- Doctor authentication (JWT)
- Patient management
- MRI image analysis workflow
- FastAPI backend with PostgreSQL
- Flutter frontend

This README is optimized for macOS setup and day-to-day development.

## Architecture

- Backend: FastAPI, SQLAlchemy, PostgreSQL, Docker
- Frontend: Flutter
- Data flow: Doctor login -> patient records -> MRI upload -> analysis history

## Repository Structure

```text
MRI-System/
├── backend/     # FastAPI API + database + Docker
├── frontend/    # Flutter client app
├── README.md
└── FIXES_SUMMARY.md
```

## macOS Prerequisites

Install and verify the following before starting:

1. Docker Desktop for Mac
2. Flutter SDK
3. Xcode Command Line Tools
4. Git

Optional (recommended for mobile dev):
- Android Studio (Android emulator/toolchain)
- Xcode app (iOS simulator/toolchain)

Quick verification:

```bash
docker --version
docker-compose --version
flutter --version
xcode-select -p
git --version
```

## Quick Start (macOS)

### 1) Start backend services

```bash
cd backend
bash start-docker.sh
```

What this does:
- Pulls and builds Docker images
- Starts API + PostgreSQL containers
- Exposes backend at http://localhost:8000

### 2) Start frontend app

Open a new terminal tab/window:

```bash
cd frontend
flutter pub get
flutter run
```

### 3) Validate system

1. Open API docs: http://localhost:8000/docs
2. Register a doctor account
3. Add a patient
4. Run MRI analysis for that patient

## Common Commands (macOS)

Run from backend directory:

```bash
# Start services
docker-compose up -d --build

# Check status
docker-compose ps

# Stream logs
docker-compose logs -f

# Stop services
docker-compose down

# Stop and remove volumes (destructive)
docker-compose down -v

# Access PostgreSQL shell
docker-compose exec db psql -U postgres -d mri_db
```

## Documentation Index

Core backend docs:
- [backend/docs/DOCKER_SETUP.md](backend/docs/DOCKER_SETUP.md)
- [backend/docs/DOCKER_COMMANDS.md](backend/docs/DOCKER_COMMANDS.md)
- [backend/docs/DOCKER_QUICK_REFERENCE.md](backend/docs/DOCKER_QUICK_REFERENCE.md)
- [backend/docs/API_DOCUMENTATION.md](backend/docs/API_DOCUMENTATION.md)
- [backend/docs/INTEGRATION_GUIDE.md](backend/docs/INTEGRATION_GUIDE.md)
- [backend/docs/COMPLETION_SUMMARY.md](backend/docs/COMPLETION_SUMMARY.md)

Additional references:
- [backend/README.md](backend/README.md)
- [FIXES_SUMMARY.md](FIXES_SUMMARY.md)

## Troubleshooting (macOS)

### Docker is running but API is unreachable

```bash
cd backend
docker-compose ps
docker-compose logs -f
```

Look for startup errors, then restart:

```bash
docker-compose down
docker-compose up -d --build
```

### Flutter toolchain issues

```bash
flutter doctor
```

Resolve reported issues, then retry:

```bash
cd frontend
flutter clean
flutter pub get
flutter run
```

### Port conflicts

If ports 8000 or 5432 are busy, stop conflicting services or update port mappings in [backend/docker-compose.yml](backend/docker-compose.yml).

## Production Notes

- Use secure, environment-specific secrets in backend .env
- Restrict CORS and allowed hosts
- Add monitoring, backups, and log aggregation
- Use managed PostgreSQL or hardened container deployment

## Status

- Version: 1.0.0
- Last updated: April 16, 2026