helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

helm show values grafana/loki-stack > values.yaml
helm install grafana-loki grafana/loki-stack -v values.yaml-n dev