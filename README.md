# 🚀 Employee Management System - DevOps CI/CD

A full-stack Employee Management application built with **React**, **Spring Boot**, and **MySQL**, containerized with **Docker**, automated with **GitHub Actions**, published to **Docker Hub**, and deployed on **Kubernetes (Kind)** using **NGINX Ingress**.

---

# 📌 Features

- Employee CRUD operations
- React frontend
- Spring Boot REST API
- MySQL database
- Dockerized services
- Docker Compose deployment
- GitHub Actions CI/CD pipeline
- Automatic Docker Hub image publishing
- Kubernetes deployment
- Persistent MySQL storage using StatefulSet
- NGINX Ingress for routing

---

# 🏗️ Architecture

```
                    Browser
                       │
             http://employee.local
                       │
               NGINX Ingress
                       │
              Frontend Service
                       │
              React Frontend Pod
                       │
                Backend Service
                       │
            Spring Boot Backend Pod
                       │
                MySQL Service
                       │
              MySQL StatefulSet
                       │
             Persistent Volume
```

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| React | Frontend |
| Spring Boot | Backend REST API |
| MySQL 8 | Database |
| Docker | Containerization |
| Docker Compose | Local multi-container deployment |
| GitHub Actions | CI/CD |
| Docker Hub | Image Registry |
| Kubernetes (Kind) | Container Orchestration |
| NGINX Ingress | Reverse Proxy |

---

# 📂 Project Structure

```
CRUD-App-CICD/
│
├── react-frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── src/
│
├── springboot-backend/
│   ├── Dockerfile
│   └── src/
│
├── kubernetes/
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── mysql-service.yaml
│   ├── mysql-statefulset.yaml
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   └── ingress.yaml
│
├── .github/
│   └── workflows/
│       └── docker-build.yml
│
├── docker-compose.yml
├── kind-config.yaml
└── README.md
```

---

# 🐳 Running with Docker Compose

## Clone repository

```bash
git clone https://github.com/filipstankovski/CRUD-App-CICD.git

cd CRUD-App-CICD
```

## Start application

```bash
docker compose up --build
```

Services:

- Frontend → http://localhost
- Backend → http://localhost:8080
- MySQL → localhost:3306

---

# ☸️ Running on Kubernetes

## Create Kind cluster

```bash
kind create cluster --name employee-cluster --config kind-config.yaml
```

## Install NGINX Ingress

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

Wait until the controller is running:

```bash
kubectl get pods -n ingress-nginx
```

---

## Deploy application

```bash
kubectl apply -f kubernetes/
```

---

## Verify deployment

```bash
kubectl get pods -n employee-app

kubectl get svc -n employee-app

kubectl get ingress -n employee-app
```

---

## Access application

Add to `/etc/hosts`

```
127.0.0.1 employee.local
```

Open:

```
http://employee.local
```

---

# ⚙️ CI/CD Pipeline

The project includes a GitHub Actions workflow that automatically:

1. Builds the Spring Boot Docker image
2. Builds the React Docker image
3. Pushes both images to Docker Hub

Workflow location:

```
.github/workflows/docker-build.yml
```

Pipeline flow:

```
Git Push
     │
     ▼
GitHub Actions
     │
     ▼
Build Docker Images
     │
     ▼
Push to Docker Hub
     │
     ▼
Kubernetes pulls latest images
```

---

# 🐋 Docker Hub Images

Backend

```
filipstankovskii/employee-backend:latest
```

Frontend

```
filipstankovskii/employee-frontend:latest
```

---

# 📸 Screenshots

Add screenshots here:

- GitHub Actions successful workflow
- Docker Hub repositories
- Docker Compose running
- Kubernetes Pods
- Kubernetes Services
- Kubernetes Ingress
- Employee Management application running

---

# 👨‍💻 Author

**Filip Stankovski**

Faculty of Computer Science and Engineering (FINKI)

DevOps / CI-CD Project