
## We need a Kubernetes cluster

ref - [kind](https://kind.sigs.k8s.io/docs/user/quick-start/)


kind create cluster --name fluentd --image kindest/node:v1.19.1

cd .\monitoring\logging\kubernetes\

#note: use your own tag!
docker build . -t logefk/fluentd-demo

#note: use your own tag!
docker push logefk/fluentd-demo


## Fluentd Namespace

kubectl create ns fluentd

# deploy configmap:

kubectl apply -f .\monitoring\logging\fluentd\kubernetes\fluentd-configmap.yaml


## Fluentd Daemonset

kubectl apply -f .\monitoring\logging\fluentd\kubernetes\fluentd-rbac.yaml 
kubectl apply -f .\monitoring\logging\fluentd\kubernetes\fluentd.yaml
kubectl -n fluentd get pods


# deploy logs example to `stdout`

kubectl apply -f .\monitoring\logging\fluentd\kubernetes\counter.yaml
kubectl get pods


## ElasticSearch and Kibana

kubectl create ns elastic-kibana

# deploy elastic search
kubectl -n elastic-kibana apply -f .\monitoring\logging\fluentd\kubernetes\elastic\elastic-search.yaml
kubectl -n elastic-kibana get pods

# deploy kibana
kubectl -n elastic-kibana apply -f .\monitoring\logging\fluentd\kubernetes\elastic\kibana.yaml
kubectl -n elastic-kibana get pods

## Kibana

kubectl -n elastic-kibana port-forward svc/kibana 5601