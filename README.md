# 🚀 DevBoard – 3-Tier Enterprise Web Application Deployment on AWS EC2 & Kubernetes

[![AWS](https://img.shields.io/badge/Cloud-AWS%20EC2-orange?style=for-the-badge&logo=amazon-aws)](https://aws.amazon.com/)
[![Kubernetes](https://img.shields.io/badge/Orchestration-Kubernetes%20%28kubectl%29-blue?style=for-the-badge&logo=kubernetes)](https://kubernetes.io/)
[![Docker](https://img.shields.io/badge/Containerization-Docker-2496ED?style=for-the-badge&logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-4169E1?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)
[![SonarQube](https://img.shields.io/badge/Code%20Quality-SonarQube-4E9BCD?style=for-the-badge&logo=sonarqube)](https://www.sonarqube.org/)

A production-grade, containerized **3-Tier Web Application (DevBoard)** hosted on an **AWS EC2** instance using **Kubernetes (`kubectl`)**, **Docker**, **Docker Compose**, and **PostgreSQL**. This project demonstrates complete lifecycle management of microservices, dynamic configuration, stateful volume management, SonarQube code quality inspection, and Makefile automation.

---

## 📌 Key Highlights & Features

* **3-Tier Microservices Architecture:** Decoupled Frontend (UI), Backend (REST API), and PostgreSQL Database.
* **Dual Execution Modes:** Supports both local orchestrations via **Docker Compose** and cluster-wide deployments via **Kubernetes (`k8/`)**.
* **Database Initialization:** Automated DB schema setup via dedicated `init/postgres` scripts.
* **DevOps Automation:** Included **`Makefile`** for quick local setup, building, and cluster deployment workflows.
* **Code Quality Assurance:** Configured **SonarQube (`sonar-project.properties`)** for static code analysis.
* **Stateful Persistence & Config:** Dynamic environment isolation using ConfigMaps, Secrets, and PersistentVolumeClaims (PVC).

---

## 📁 Repository Directory Structure

```text
Devboard-3tier-k8s-Deployment/
├── backend/                    # Backend API microservice source code & Dockerfile
├── frontend/                   # Frontend UI web app source code & Dockerfile
├── init/                       # Database initialization resources
│   └── postgres/               # SQL scripts & DB setup files
├── k8/                         # Kubernetes Configuration Manifests
│   ├── namespace.yml           # Isolated 'devboard' namespace
│   ├── configmap.yml           # Environment configuration variables
│   ├── secret.yml              # Database credentials (Base64)
│   ├── persistent-volume.yml   # Volume definition
│   ├── persistent-volume-claim.yml # Storage request claim
│   ├── postgres-service.yml    # Database Service endpoint
│   ├── postgres-statefulset.yml# PostgreSQL StatefulSet deployment
│   ├── backend-deployment.yml  # Backend API deployment
│   ├── frontend-deployment.yml # Frontend UI deployment
│   └── service.yml             # External & Internal Service definitions
├── .dockerignore               # Docker build exclusion patterns
├── .env.example                # Sample environment variables template
├── .gitignore                  # Git untracked files & secrets filter
├── docker-compose.yml          # Multi-container Docker compose manifest
├── Makefile                    # Automation task shortcuts
├── sonar-project.properties    # SonarQube static code scanner configuration
└── README.md                   # Comprehensive project documentation
