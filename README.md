# Dockerized Flask Application with Nginx Reverse Proxy and CI/CD Deployment
## Overview

This project demonstrates how a simple web application can be containerized, reverse-proxied, deployed, and debugged using modern DevOps tooling.
The focus of this project is infrastructure behavior and deployment workflows, not backend complexity. A minimal Flask application is intentionally used so the emphasis remains on:
- Container networking
- Reverse proxy architecture
- Traffic flow
- Infrastructure debugging
- CI/CD automation
- Cloud deployment on AWS

## Tech Stack
- Docker
- Docker Compose
- Nginx (Reverse Proxy)
- Flask (minimal workload)
- GitHub Actions (CI/CD)
- Docker Hub (Image Registry)
- AWS EC2 (Cloud Deployment)
- Linux (Amazon Linux)

## Architecture
→ Client (Browser)

→ Host Machine (Port 80)

→ Nginx Container (Reverse Proxy)

→ Flask App Container (Port 5000)

→ HTTP Response

## Project Structure
```bash
dockerized-flask-nginx/
│
├── app/
│   └── app.py
│
├── nginx/
│   └── nginx.conf
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── Dockerfile
├── docker-compose.yml
├── README.md
└── .gitignore
```
## Running Locally
Clone the repository:
```bash
git clone https://github.com/Juhee2306/dockerized-flask-nginx
cd dockerized-flask-nginx
```
Start the application:
```bash
docker compose up --build
```
Access:
```bash
http://localhost
```
## CI/CD Pipeline
The project includes an automated deployment pipeline using GitHub Actions.
Pipeline workflow:
```bash
Git Push
   ↓
GitHub Actions
   ↓
Build Docker Image
   ↓
Push Image to Docker Hub
   ↓
SSH into AWS EC2
   ↓
docker compose pull
   ↓
docker compose up -d
```
This allows the application to update automatically after every commit.
## Cloud Deployment
The application runs on an AWS EC2 instance (Amazon Linux).
Security group configuration:
```bash
Port 22  → SSH
Port 80  → HTTP
```
Public architecture:
```bash
Client → Internet → EC2 → Nginx → Flask
```
## DevOps Concepts Demonstrated

- Docker containerization
- Multi-container orchestration
- Reverse proxy architecture
- Docker networking
- CI/CD automation
- Remote deployment with SSH
- Cloud infrastructure on AWS
## Example Failure Scenario
Stopping the Flask container results in:
502 Bad Gateway
### Diagnosis:
docker compose logs nginx
### Learning:
Reverse proxies depend on upstream services being available.
## Outcome
A production-style containerized system with:
- Nginx reverse proxy
- Flask application
- Docker Compose orchestration
- CI/CD deployment pipeline
- AWS EC2 hosting



