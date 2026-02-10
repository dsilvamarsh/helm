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

###Open telimetary operator
https://github.com/open-telemetry/opentelemetry-helm-charts/tree/main/charts/opentelemetry-operator

### Install cert manager
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.19.2/cert-manager.yaml

helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
helm repo update

helm install opentelemetry-operator open-telemetry/opentelemetry-operator \
--set "manager.collectorImage.repository=ghcr.io/open-telemetry/opentelemetry-collector-releases/opentelemetry-collector-k8s" \
--namespace infra-services \
--set admissionWebhooks.certManager.enabled=false \
--set admissionWebhooks.autoGenerateCert.enabled=true

### Install the collector
kubectl apply -f open-telemetry-collector/deployment.yaml -n infra-services


###Cleanup
helm uninstall opentelemetry-operator
kubectl delete crd opentelemetrycollectors.opentelemetry.io
kubectl delete crd opampbridges.opentelemetry.io
kubectl delete crd instrumentations.opentelemetry.io
kubectl delete crd targetallocators.opentelemetry.io