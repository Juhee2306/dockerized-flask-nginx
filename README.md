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
