
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
helm upgrade --install traefik traefik/traefik   -n infra-services  -f traefic-kubernates-gateway/values.yaml
