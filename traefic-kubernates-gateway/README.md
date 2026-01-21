
https://docs.siderolabs.com/kubernetes-guides/advanced-guides/deploy-traefik

Directly install from the helm chart which will install the CRD 

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
helm upgrade --install traefik traefik/traefik   -n dev  -f traefic-kubernates-gateway/values.yaml


  # Apply the Deployment Gateway
  kubectl apply -f traefic-kubernates-gateway/api-gw-deployment.yaml



  #uninstall Gateway 

  helm upgrade --uninstall traefik traefik/traefik \
  -n traefik --create-namespace \
  -f values.yaml


  kubectl get --namespace dev gateway/traefik-gateway -o yaml