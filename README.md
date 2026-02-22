# Dockerized Flask App with Nginx Reverse Proxy
## Overview

This project demonstrates how a simple web application is run, exposed, proxied, and debugged using Docker, Docker Compose, and Nginx.
The goal of this project is not backend development, but to understand application runtime behavior, container networking, traffic flow,
and real-world debugging scenarios that DevOps and Cloud engineers encounter in production systems.
A minimal Flask app is used intentionally so the focus remains on infrastructure, not application logic

## Tech Stack
- Docker
- Docker Compose
- Nginx (Reverse Proxy)
- Flask (minimal workload)
- Linux

## Architecture
→ Client (Browser)

→ Host Machine (Port 80)

→ Nginx Container (Reverse Proxy)

→ Flask App Container (Port 5000)

→ HTTP Response

## Project Structure
```bash
dockerized-flask-nginx/
├── app/
│   └── app.py
├── nginx/
│   └── nginx.conf
├── Dockerfile
├── docker-compose.yml
├── .gitignore
└── README.md

```
## How It Works
- The Flask app runs inside a Docker container and listens on port 5000.
- Nginx runs in a separate container and listens on port 80.
- Nginx forwards incoming HTTP requests to the Flask app using:
```bash
proxy_pass http://app:5000;
```
- Docker Compose:
1. Creates a shared network
2. Provides automatic service discovery
3. Manages both containers as a single system

## Running the Project
```bash
docker compose up --build
```
Access the Application at:
```bash
http://localhost
```
## Intentional Failures & Debugging
This project includes deliberate failure scenarios to practice real-world debugging.

1. Flask Container Stopped

Result: Browser returns 502 Bad Gateway
Diagnosis:
```bash
docker ps
docker compose logs nginx
```
Learning: A reverse proxy depends on the upstream service being available.

2. Port Mismatch in Nginx Configuration

Changed the upstream port in nginx.conf
Result: Nginx starts successfully but cannot reach Flask
Diagnosis:
```bash
docker compose logs nginx
```

Learning: Many production failures are caused by port misconfiguration, not code issues.

3. Bind Mount Restart Failure (Docker Desktop / WSL)

Restarting Nginx failed due to a bind-mounted configuration file

Correct fix:
```bash
docker compose down
docker compose up --build
```
Learning: Containers are disposable — recreating them is safer than restarting broken infrastructure.

## Key Learnings

- Difference between host ports and container ports
- Why application servers should not face the internet directly
- Role of Nginx as a reverse proxy
- Docker networking and service-name DNS
- Using logs to diagnose failures instead of reinstalling blindly
- Treating infrastructure as reproducible and disposable

## Outcome
A working, production-style containerized setup with:
- Clean traffic flow
- Proper separation of concerns
- Debuggable failure scenarios
- Clear understanding of runtime behavior
