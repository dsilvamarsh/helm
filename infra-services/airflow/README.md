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




### Create Postgres DB
-- Database: airflow

-- DROP DATABASE IF EXISTS airflow;

CREATE DATABASE airflow
    WITH
    OWNER = airflow_user
    ENCODING = 'UTF8'
    LC_COLLATE = 'en_US.UTF-8'
    LC_CTYPE = 'en_US.UTF-8'
    LOCALE_PROVIDER = 'libc'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;

GRANT TEMPORARY, CONNECT ON DATABASE airflow TO PUBLIC;

GRANT ALL ON DATABASE airflow TO airflow_user;

GRANT ALL PRIVILEGES ON DATABASE airflow TO airflow_user;