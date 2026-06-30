# Employee Management System - DevOps CI/CD

A full-stack Employee Management application built with **React**, **Spring Boot**, and **MySQL**, containerized with **Docker**, automated with **GitHub Actions**, published to **Docker Hub**, and deployed on **Kubernetes (Kind)** using **NGINX Ingress**.

---

# Author

**Filip Stankovski 233111**

Faculty of Computer Science and Engineering (FINKI)

DevOps / CI-CD Project

---

# Features

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

# Architecture

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

# Technologies Used

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

# Project Structure

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

# Running with Docker Compose

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

# Running on Kubernetes

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

# CI/CD Pipeline

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

# Docker Hub Images

Backend

```
filipstankovskii/employee-backend:latest
```

Frontend

```
filipstankovskii/employee-frontend:latest
```

---

# Screenshots

Add screenshots here:

- GitHub Actions successful workflow
  <img width="1885" height="955" alt="3 GITHUB_Actions" src="https://github.com/user-attachments/assets/28fee96d-9dc9-424d-8a6c-c5dfbb392892" />

- Docker Hub repositories
  <img width="1920" height="378" alt="4 DockerHub" src="https://github.com/user-attachments/assets/ea01175b-7ef0-4b2b-9a45-0da14c5b16f7" />

- Docker Compose running
  <img width="1919" height="510" alt="2 docker_images" src="https://github.com/user-attachments/assets/b9b42645-1063-45de-a012-138a6037d085" />
  <img width="1624" height="331" alt="1 docker compose up" src="https://github.com/user-attachments/assets/e7c72091-f17a-4d32-86c6-cac8b804b914" />

- Kubernetes Pods
  <img width="1427" height="137" alt="5 Kubec Pods" src="https://github.com/user-attachments/assets/ec7d3f35-64c1-4dc0-a775-5e0604621c34" />

- Kubernetes Services
  <img width="1262" height="143" alt="6 Kubernetes Services" src="https://github.com/user-attachments/assets/d528e27a-9590-42a1-8e04-2b781280558d" />

- Kubernetes Ingress
  <img width="1236" height="93" alt="7 Kubernetes Ingress" src="https://github.com/user-attachments/assets/7b0a4fa7-bde9-406a-8b9e-11eacd228662" />

- Employee Management application running
  <img width="1601" height="935" alt="Screenshot_1" src="https://github.com/user-attachments/assets/91f8cb2f-c277-4b8c-8c7b-ce6ed9be75fb" />
  
## GitOps Continuous Deployment with Argo CD

The project uses **Argo CD** to implement Continuous Deployment following the GitOps approach. Kubernetes manifests stored in the GitHub repository are continuously monitored, and any changes are automatically synchronized to the Kubernetes cluster.

The dashboard below shows the application in a **Healthy** and **Synced** state.
  
  <img width="1920" height="1028" alt="image" src="https://github.com/user-attachments/assets/b8b175b8-0d1a-4154-941b-d168d908a7e7" />


