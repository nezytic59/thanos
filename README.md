# thanos
multi-cluster monitoring

## Edge-cluster

```
$ kubectl create ns monitoring
```
* Change Value Like data-producer-1,2,...
```
$ helm install kube-prometheus bitnami/kube-prometheus --set prometheus.thanos.create=true --set operator.service.type=ClusterIP --set prometheus.service.type=ClusterIP --set alertmanager.service.type=ClusterIP --set prometheus.thanos.service.type=LoadBalancer --set prometheus.externalLabels.cluster="data-producer-1" -n monitoring
```

## Core-cluster
```
$ git clone https://github.com/59nezytic/thanos.git
```
```
$ cd thanos
```
* Edit values.yaml for your own settings. <YOUR_EDGE_MASTER_1_IP>
```
$ kubectl create ns monitoring
```
```
$ helm install kube-prometheus bitnami/kube-prometheus --set prometheus.thanos.create=true --set operator.service.type=ClusterIP --set prometheus.service.type=ClusterIP --set alertmanager.service.type=ClusterIP --set prometheus.thanos.service.type=LoadBalancer -n monitoring
```
```
$ helm install grafana bitnami/grafana --set service.type=NodePort --set admin.password=<YOUR_PASSWORD> --set persistence.enabled=false -n monitoring
```
```
$ helm install thanos --values values.yaml --namespace monitoring bitnami/thanos --version 5.3.0
```

## Grafana Dashboard
* Check your 'thanos-query' Service IP -> This is your Data Sources URL
![image](https://user-images.githubusercontent.com/55429907/139818900-1dfa8081-9415-4f55-b4ff-a1d754b33be4.png)
* Create-import-import via panel json (This file is 'grafana-dashboard-thanos.json', so copy and paste it)
* Load
* Finish!
![image](https://user-images.githubusercontent.com/55429907/139819147-e8b32e45-3a6d-4477-b22a-f2ceb9b2ff07.png)
