
https://docs.siderolabs.com/kubernetes-guides/advanced-guides/deploy-traefik

https://github.com/traefik/traefik-helm-chart

#Create a file in a dir
cat << EOF > values.yaml
providers:
  kubernetesGateway:
    enabled: true
EOF

#Apply the below commands 
NOTE: we can create our own namesapce and replace it in the -n option
helm repo add traefik https://traefik.github.io/charts
helm repo update
helm install  traefik traefik/traefik   -n infra-services  -f traefic-kubernates-gateway/values.yaml
helm upgrade  traefik traefik/traefik   -n infra-services  -f traefic-kubernates-gateway/values.yaml


kubectl create secret tls keycloak-tls-secret --cert keycloak.learning.localhost.com.crt --key keycloak.learning.localhost.com.pem -n infra-services


openssl genrsa -aes256 -out traefik.learning.localhost.com.key 2048

password : changeit

openssl req -new -key traefik.learning.localhost.com.key -subj "/C=IN/ST=Maharashtra/L=Mumbai/O=Onepiece/OU=Security Dept/CN=traefik.learning.localhost.com" -out traefik.learning.localhost.com.csr

openssl x509 -req -extfile <(printf "subjectAltName=DNS:traefik.learning.localhost.com,IP:127.0.0.1") -in traefik.learning.localhost.com.csr -CA root_ca.pem -CAkey root_ca.key -CAcreateserial -out traefik.learning.localhost.com.crt -days 3650 -sha256


openssl pkcs12 -export -in traefik.learning.localhost.com.crt -inkey traefik.learning.localhost.com.key -out traefik-keystore.p12 -name server -CAfile root_ca.pem -caname rootCA
password : changeit

we need to load the key and the certificate in kubernates secret to be able to load it to traefik
openssl rsa -in traefik.learning.localhost.com.key -out traefik.learning.localhost.com.pem

kubectl create secret tls traefik-tls-secret --cert traefik.learning.localhost.com.crt --key traefik.learning.localhost.com.pem -n infra-services