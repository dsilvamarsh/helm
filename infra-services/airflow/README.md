# APACHE AIRFLOW 
https://airflow.apache.org/docs/helm-chart/stable/index.html

helm repo add apache-airflow https://airflow.apache.org
helm install airflow apache-airflow/airflow -f airflow/values.yaml --namespace infra-services 
helm upgrade airflow apache-airflow/airflow -f airflow/values.yaml --namespace infra-services 
helm uninstall airflow --namespace infra-services 

### Airflow cleanup

helm delete airflow --namespace infra-services
kubectl delete pvc -n airflow logs-gta-triggerer-0
kubectl delete pvc -n airflow logs-gta-worker-0
kubectl delete pvc -n airflow redis-db-gta-redis-0


