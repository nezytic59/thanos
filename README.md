# thanos
multi-cluster monitoring

## Edge-cluster

```
kubectl create ns monitoring
```
* Change Value Like data-producer-1,2,...
```
helm install kube-prometheus bitnami/kube-prometheus --set prometheus.thanos.create=true --set operator.service.type=ClusterIP --set prometheus.service.type=ClusterIP --set alertmanager.service.type=ClusterIP --set prometheus.thanos.service.type=LoadBalancer --set prometheus.externalLabels.cluster="data-producer-1" -n monitoring
```

## Core-cluster
```
git clone https://github.com/59nezytic/thanos.git
```
```
cd thanos
```
```
kubectl create ns monitoring
```
```
helm install kube-prometheus bitnami/kube-prometheus --set prometheus.thanos.create=true --set operator.service.type=ClusterIP --set prometheus.service.type=ClusterIP --set alertmanager.service.type=ClusterIP --set prometheus.thanos.service.type=LoadBalancer -n monitoring
```
```
helm install grafana bitnami/grafana --set service.type=NodePort --set admin.password=awdxsqeqe1! --set persistence.enabled=false -n monitoring
```
```
helm install thanos --values values.yaml --namespace monitoring bitnami/thanos --version 5.3.0
```
