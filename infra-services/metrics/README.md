# Metrics Infrastructure Service

This repository manages the deployment of **Loki,Grafana,Prometheus** on Kubernetes using the [Bitnami PostgreSQL Helm Chart](https://artifacthub.io). This setup is intended for shared infrastructure services.

## 📋 Prerequisites

- **Kubernetes Cluster** (v1.23+)
- **Helm CLI** (v3.0+) [Installation Guide](https://helm.sh)
- **kubectl** configured to your cluster

## 🚀 Installation

### 1. Create the Namespace
Isolate the database by creating a dedicated namespace for infrastructure services:
```bash
kubectl create namespace infra-services

### 2. Install Loki 
helm install loki grafana/loki  -f loki/values.yaml -n infra-services
### 3. Install Prometheus which will install grafan as well
helm install prometheus prometheus-community/kube-prometheus-stack   -f prometheus/values.yaml -n infra-services


install grafana 
https://grafana.com/docs/grafana/latest/setup-grafana/installation/helm/