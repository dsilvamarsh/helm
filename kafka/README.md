https://strimzi.io/quickstarts/

kubectl create namespace kafka
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka

kubectl apply -f kafka-single-node.yaml -n kafka 

produce messages to kafka 

kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.50.0-kafka-4.1.1 --rm=true --restart=Never -- bin/kafka-console-producer.sh --bootstrap-server kafka-cluster-kafka-bootstrap:9092 --topic my-topic

consume messsages from kafka

kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.50.0-kafka-4.1.1 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server kafka-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning



http://kafka-cluster-kafka-bootstrap.dev.svc.cluster.local/
