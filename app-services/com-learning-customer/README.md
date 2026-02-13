helm install com-learning-customer ./com-learning-customer -n app-services   

helm upgrade com-learning-customer ./com-learning-customer -n app-services   

helm uninstall com-learning-customer -n app-services 



export APP_HOSTNAME=com-learning-customer.localhost
    echo "Visit http://$APP_HOSTNAME/ to use your application"


Test in postman 
    curl --location 'http://localhost:80/exchange-rate' \
--header 'Host: com-learning-customer.localhost'