https://artifacthub.io/packages/helm/postgres/postgres

kubectl create namespace infra-services

helm install postgres -f values.yaml bitnami/postgresql -n infra-services

