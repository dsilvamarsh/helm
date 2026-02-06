openssl genrsa -aes128 -out alice_private.pem 1024

private key pass : alice_private

openssl rsa -in alice_private.pem -pubout > alice_public.pem



openssl genrsa -aes128 -out bob_private.pem 1024

private key pass : bob_private

echo "welcome to tls " > welcome.txt

openssl pkeyutl -encrypt -inkey bob_public.pem -pubin -in welcome.txt -out welcome_secret.enc


openssl pkeyutl -decrypt -inkey  bob_private.pem -in welcome_secret.enc -out welcome_decoded.txt


root ca signing
https://gist.github.com/elklein96/a15090f35a41e16bdc8574a7fb81e119


openssl genrsa -aes256 -out root_ca.key 2048

password : changeit

openssl req -x509 -new -key root_ca.key -sha256 -days 1024  -subj "/C=IN/ST=Maharashtra/L=Mumbai/O=Onepiece/OU=Training Dept/CN=learning.localhost.com" -out root_ca.pem



openssl genrsa -aes256 -out ingress.learning.localhost.com.key 2048

password : changeit

openssl req -new -key ingress.learning.localhost.com.key -subj "/C=IN/ST=Maharashtra/L=Mumbai/O=Onepiece/OU=Training Dept/CN=ingress.learning.localhost.com" -out ingress.learning.localhost.com.csr

openssl x509 -req -extfile <(printf "subjectAltName=DNS:ingress.learning.localhost.com,IP:127.0.0.1") -in ingress.learning.localhost.com.csr -CA root_ca.pem -CAkey root_ca.key -CAcreateserial -out ingress.learning.localhost.com.crt -days 3650 -sha256


openssl pkcs12 -export -in ingress.learning.localhost.com.crt -inkey ingress.learning.localhost.com.key -out ingress-keystore.p12 -name server -CAfile root_ca.pem -caname rootCA
password : changeit



# Keycloak host and TLS certificate
openssl genrsa -aes256 -out keycloak.learning.localhost.com.key 2048

password : changeit

openssl req -new -key keycloak.learning.localhost.com.key -subj "/C=IN/ST=Maharashtra/L=Mumbai/O=Onepiece/OU=Security Dept/CN=keycloak.learning.localhost.com" -out keycloak.learning.localhost.com.csr

openssl x509 -req -extfile <(printf "subjectAltName=DNS:keycloak.learning.localhost.com,IP:127.0.0.1") -in keycloak.learning.localhost.com.csr -CA root_ca.pem -CAkey root_ca.key -CAcreateserial -out keycloak.learning.localhost.com.crt -days 3650 -sha256


openssl pkcs12 -export -in keycloak.learning.localhost.com.crt -inkey keycloak.learning.localhost.com.key -out keycloak-keystore.p12 -name server -CAfile root_ca.pem -caname rootCA
password : changeit