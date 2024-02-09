
# INSTALLATION the k8S way:


https://strimzi.io/quickstarts/
=>
kubectl create namespace kafka
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka
kubectl get pod -n kafka --watch
Get kafka-ephemeral.yaml from https://github.com/strimzi/strimzi-kafka-operator/blob/ac80e5f5613cbfc885e5a168e0e14387cd2a2614/packaging/examples/kafka/kafka-ephemeral-single.yaml
kubectl apply -f k8s/part1/kafka-ephemeral.yaml -n kafka

kubectl get all -n kafka
=>
pod/my-kafka-cluster-entity-operator-7bb9fd4f56-7k28w   2/2     Running   0          57s
pod/my-kafka-cluster-kafka-0                            1/1     Running   0          82s
pod/my-kafka-cluster-zookeeper-0                        1/1     Running   0          106s
pod/my-kafka-cluster-zookeeper-1                        1/1     Running   0          106s
pod/my-kafka-cluster-zookeeper-2                        1/1     Running   0          106s
pod/strimzi-cluster-operator-7b6bcddf-j8d98       1/1     Running   0          4m46s

NAME                                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                               AGE
service/my-kafka-cluster-kafka-bootstrap    ClusterIP   10.97.238.97     <none>        9091/TCP,9092/TCP                     83s
service/my-kafka-cluster-kafka-brokers      ClusterIP   None             <none>        9090/TCP,9091/TCP,8443/TCP,9092/TCP   83s
service/my-kafka-cluster-zookeeper-client   ClusterIP   10.100.239.206   <none>        2181/TCP                              108s
service/my-kafka-cluster-zookeeper-nodes    ClusterIP   None             <none>        2181/TCP,2888/TCP,3888/TCP            108s

NAME                                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/my-kafka-cluster-entity-operator   1/1     1            1           57s
deployment.apps/strimzi-cluster-operator     1/1     1            1           4m46s

NAME                                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/my-kafka-cluster-entity-operator-7bb9fd4f56   1         1         1       57s
replicaset.apps/strimzi-cluster-operator-7b6bcddf       1         1         1       4m46s


kubectl get configmap/my-kafka-cluster-kafka-0 -n kafka -o yaml (Bug for configmap name)
kubectl get configmap/my-kafka-cluster-zookeeper-config -n kafka -o yaml

PRODUCER:
kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.39.0-kafka-3.6.1 --rm=true --restart=Never -- bin/kafka-console-producer.sh --bootstrap-server my-kafka-cluster-kafka-bootstrap:9092 --topic my-topic
CONSUMER:
kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.39.0-kafka-3.6.1 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-kafka-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning


export CLUSTER_NAME=my-kafka-cluster
kubectl get configmap/${CLUSTER_NAME}-kafka-config -o yaml


DELETION:
kubectl -n kafka delete $(kubectl get strimzi -o name -n kafka)
kubectl -n kafka delete -f 'https://strimzi.io/install/latest?namespace=kafka'



Ou bien https://itnext.io/kafka-on-kubernetes-the-strimzi-way-part-1-bdff3e451788
avec Helm pour installer strimzi
Puis appliquer le yaml suivant pour un simple cluster Kafka avec Zk sans persistance


https://aws.amazon.com/fr/blogs/containers/deploying-and-scaling-apache-kafka-on-amazon-eks/

new comment for feature branch


Run /home/runner/work/_actions/wangchucheng/git-repo-sync/v0.1.0/entrypoint.sh
  /home/runner/work/_actions/wangchucheng/git-repo-sync/v0.1.0/entrypoint.sh
  shell: /usr/bin/bash --noprofile --norc -e -o pipefail {0}
  env:
    INPUT_TARGET_URL: 
    INPUT_TARGET_USERNAME: 
    INPUT_TARGET_TOKEN: 
    GITHUB_EVENT_REF: refs/heads/main
fatal: unable to access 'https:///': URL using bad/illegal format or missing URL


