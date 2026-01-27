kubectl create namespace infra-services
not mandatory
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.18.2/cert-manager.yaml

helm repo add flink-operator-repo https://downloads.apache.org/flink/flink-kubernetes-operator-1.13.0/

helm install flink-kubernetes-operator -f values.yaml flink-operator-repo/flink-kubernetes-operator -n infra-services 