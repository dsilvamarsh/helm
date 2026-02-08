# PostgreSQL Infrastructure Service

This repository manages the deployment of **PostgreSQL** on Kubernetes using the [Bitnami PostgreSQL Helm Chart](https://artifacthub.io). This setup is intended for shared infrastructure services.

## 📋 Prerequisites

- **Kubernetes Cluster** (v1.23+)
- **Helm CLI** (v3.0+) [Installation Guide](https://helm.sh)
- **kubectl** configured to your cluster

## 🚀 Installation

### 1. Create the Namespace
Isolate the database by creating a dedicated namespace for infrastructure services:
```bash
kubectl create namespace infra-services

Refrences : https://artifacthub.io/packages/helm/postgres/postgres

kubectl create namespace infra-services

helm install postgres -f postgres/values.yaml bitnami/postgresql -n infra-services




