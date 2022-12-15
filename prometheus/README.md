Install Prometheus Helm Chart (with Grafana)
Source: https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

```
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm search repo kube-prometheus
# use default value
$ helm inspect values prometheus-community/kube-prometheus-stack > /tmp/kube-prometheus-stack.values
$ helm install prometheus-community/kube-prometheus-stack --create-namespace --namespace prometheus --generate-name --values /tmp/kube-prometheus-stack.values
```
