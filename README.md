# 🚀 DevBoard – 3-Tier Enterprise Web Application Deployment on AWS EC2 & Kubernetes

[![AWS](https://img.shields.io/badge/Cloud-AWS%20EC2-orange?style=for-the-badge&logo=amazon-aws)](https://aws.amazon.com/)
[![Kubernetes](https://img.shields.io/badge/Orchestration-Kubernetes%20%28kubectl%29-blue?style=for-the-badge&logo=kubernetes)](https://kubernetes.io/)
[![Docker](https://img.shields.io/badge/Containerization-Docker-2496ED?style=for-the-badge&logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-4169E1?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)

A production-grade, containerized **3-Tier Web Application (DevBoard)** hosted on an **AWS EC2** instance using **Kubernetes (`kubectl`)**, **Docker**, and **PostgreSQL**. This project demonstrates complete lifecycle management of microservices, dynamic configuration, stateful volume management, and internal DNS service discovery.

---

## 📌 Project Overview & Features

* **3-Tier Microservices Architecture:** Isolated Frontend (UI), Backend (REST API), and Database layers.
* **Namespace Isolation:** All application components are isolated within a dedicated `devboard` Kubernetes namespace.
* **Configuration Management:** Decoupled app configuration using **ConfigMaps** and sensitive credentials using **Kubernetes Secrets**.
* **Stateful Persistence:** Reliable database persistence configured with **PersistentVolume (PV)** and **PersistentVolumeClaim (PVC)**.
* **Internal Service Discovery:** Decoupled inter-service communication via Headless & ClusterIP Services.
* **External Access:** Exposed application traffic to external users via NodePort / Port-Forwarding with AWS EC2 Inbound Security Rules.

---

## 📐 Architecture Diagram

```text
                               ┌──────────────────────────────────────────────────────────┐
                               │                    AWS EC2 INSTANCE                      │
                               │                                                          │
   [ User Browser ]            │    ┌────────────────────────────────────────────────┐    │
          │                    │    │             KUBERNETES CLUSTER                 │    │
          │ (Port 8081)        │    │           (Namespace: devboard)                │    │
          ▼                    │    │                                                │    │
┌──────────────────┐           │    │  ┌─────────────────┐                           │    │
│  AWS Security    │───────────┼────┼─►│ Frontend Service│                           │    │
│      Group       │           │    │  └────────┬────────┘                           │    │
└──────────────────┘           │    │           │                                    │    │
                               │    │           ▼                                    │    │
                               │    │  ┌─────────────────┐     (REST API Calls)      │    │
                               │    │  │  Frontend Pod   │──────────────────┐        │    │
                               │    │  └─────────────────┘                  │        │    │
                               │    │                                       ▼        │    │
                               │    │                           ┌──────────────────┐ │    │
                               │    │                           │ Backend Service  │ │    │
                               │    │                           └────────┬─────────┘ │    │
                               │    │                                    │           │    │
                               │    │                                    ▼           │    │
                               │    │                           ┌──────────────────┐ │    │
                               │    │                           │   Backend Pod    │ │    │
                               │    │                           └────────┬─────────┘ │    │
                               │    │                                    │           │    │
                               │    │                                    │ (Postgres │    │
                               │    │                                    │  DNS Host)│    │
                               │    │                                    ▼           │    │
                               │    │                           ┌──────────────────┐ │    │
                               │    │                           │ Postgres Service │ │    │
                               │    │                           └────────┬─────────┘ │    │
                               │    │                                    │           │    │
                               │    │                                    ▼           │    │
                               │    │                           ┌──────────────────┐ │    │
                               │    │                           │ PostgreSQL Pod   │ │    │
                               │    │                           └────────┬─────────┘ │    │
                               │    │                                    │           │    │
                               │    │                                    ▼           │    │
                               │    │                           ┌──────────────────┐ │    │
                               │    │                           │ PV / PVC Storage │ │    │
                               │    │                           └──────────────────┘ │    │
                               │    └────────────────────────────────────────────────┘    │
                               └──────────────────────────────────────────────────────────┘
