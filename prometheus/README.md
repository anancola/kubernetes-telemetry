Install Prometheus Helm Chart: kube-prometheus-stack  

Source: https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack  

Default values: https://github.com/prometheus-community/helm-charts/blob/main/charts/kube-prometheus-stack/values.yaml  

```
$ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
$ helm search repo kube-prometheus

### use default values
$ helm inspect values prometheus-community/kube-prometheus-stack > /tmp/kube-prometheus-stack.values
### use custom values with NodePort enabled
$ wget https://raw.githubusercontent.com/anancola/kubernetes-telemetry/main/prometheus/kube-prometheus-stack.values

$ helm install prometheus-community/kube-prometheus-stack --create-namespace --namespace prometheus --generate-name --values /tmp/kube-prometheus-stack.values
$ kubectl apply -f https://raw.githubusercontent.com/anancola/kubernetes-telemetry/main/prometheus/gafana-patch.yaml
$ kubectl get svc -n prometheus

```
![image](https://user-images.githubusercontent.com/6374885/207763236-f70ca0e6-ebde-47f1-b100-4f36071ff367.png)
