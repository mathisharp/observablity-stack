# alert,k8 metrics,system metrics

kind create cluster --name prometheus --image kindest/node:v1.18.4

kubectl create ns monitoring

# Create the operator 
kubectl -n monitoring apply -f ./monitoring/prometheus/kubernetes/1.18.4/prometheus-operator/

# Deploy monitoring components
kubectl -n monitoring apply -f ./monitoring/prometheus/kubernetes/1.18.4/node-exporter/
kubectl -n monitoring apply -f ./monitoring/prometheus/kubernetes/1.18.4/kube-state-metrics/
kubectl -n monitoring apply -f ./monitoring/prometheus/kubernetes/1.18.4/alertmanager

# Deploy prometheus instance
kubectl -n monitoring apply -f ./monitoring/prometheus/kubernetes/1.18.4/prometheus-cluster-monitoring/

# Dashboard
kubectl -n monitoring create -f ./monitoring/prometheus/kubernetes/1.18.4/grafana/

# references took

 (https://github.com/prometheus-operator/kube-prometheus/tree/v0.6.0/manifests)