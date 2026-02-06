Install the Operator first in the default sapce

https://www.keycloak.org/operator/installation

kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/26.5.2/kubernetes/keycloaks.k8s.keycloak.org-v1.yml
kubectl apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/26.5.2/kubernetes/keycloakrealmimports.k8s.keycloak.org-v1.yml



kubectl create namespace infra-services
kubectl -n infra-services apply -f https://raw.githubusercontent.com/keycloak/keycloak-k8s-resources/26.5.2/kubernetes/kubernetes.yml



https://www.keycloak.org/operator/basic-deployment

FOR TLS secured connections make a host entry in local machine
127.0.0.1       keycloak.learning.localhost.com

ROOT CA is created in the CERTIFICATE.md of this repo which is used to sign the certificate
convert the keycloak.learning.localhost.com.key >>  keycloak.learning.localhost.com.pem using command 

openssl rsa -in keycloak.learning.localhost.com.key -out keycloak.learning.localhost.com.pem

kubectl create secret tls keycloak-tls-secret --cert keycloak.learning.localhost.com.crt --key keycloak.learning.localhost.com.pem -n infra-services

convert secrets to base64

echo -n 'keycloak' | base64

kubectl apply -f db-secret.yaml -n infra-services

echo -n 'admin' | base64

kubectl apply -f admin-secret.yaml -n infra-services

kubectl apply -f keycloak.yaml -n infra-services


we need to expose the keycloak 
for testing we are doing a port forward 
kubectl port-forward service/keycloak-learning-service 8443:8443 -n infra-services