helm install com-learning-exchange-rate ./com-learning-exchange-rate -n dev  

helm upgrade com-learning-exchange-rate ./com-learning-exchange-rate -n dev  

helm uninstall com-learning-exchange-rate -n dev



export APP_HOSTNAME=com-learning-exchange-rate.localhost
    echo "Visit http://$APP_HOSTNAME/ to use your application"


Test in postman 
    curl --location 'http://localhost:80/exchange-rate' \
--header 'Host: com-learning-exchange-rate.localhost'