# 🚀 Jenkins with Docker, Nginx, Prometheus, and Grafana

This setup provides a **Jenkins CI/CD environment** running inside Docker, with monitoring via **Prometheus & Grafana**, and a **reverse proxy using Nginx**.

## 📌 Prerequisites
Make sure you have installed:
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 📂 Project Structure
```
.
├── docker-compose.yml      # Docker Compose configuration
├── Dockerfile              # Custom Jenkins image with Docker CLI
├── nginx/                  # Nginx configuration
│   ├── jenkins.conf        # Reverse proxy settings
├── prometheus/
│   ├── prometheus.yml      # Prometheus configuration
└── README.md               # This file
```

## 🚀 How to Run
### 1️⃣ Build Custom Jenkins Image
Before running Docker Compose, build the custom Jenkins image:
```sh
docker build -t myjenkins-blueocean:latest .
```

### 2️⃣ Start Services with Docker Compose
Run the following command to start all services:
```sh
docker-compose up -d
```
This will start:
- **Jenkins Blue Ocean UI** on `http://localhost:8080`
- **Docker Daemon (DinD)** for Jenkins builds
- **Nginx** as a reverse proxy on `http://localhost`
- **Prometheus** for monitoring on `http://localhost:9090`
- **Grafana** for visualization on `http://localhost:3030`

### 3️⃣ Get Jenkins Initial Admin Password
After the services are running, retrieve the Jenkins admin password:
```sh
docker logs jenkins-blueocean | grep -A 5 'Please use the following password'
```
Copy the password and use it to log in at `http://localhost:8080`.

### 4️⃣ Stop Services
To stop and remove all running containers:
```sh
docker-compose down
```

## 📊 Monitoring with Prometheus & Grafana
- **Prometheus UI** → `http://localhost:9090`
- **Grafana UI** → `http://localhost:3030`
  - Default login: `admin / admin`
  - You can add Prometheus as a data source in Grafana.

## 🎯 Notes
- This setup is for **development/testing** purposes. For production, secure Jenkins and limit `privileged` access.
- Modify the `nginx/jenkins.conf` file to customize reverse proxy settings.

Happy coding! 🚀