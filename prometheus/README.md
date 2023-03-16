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

# The Units
CPU: 1m core= 1/1000 core, 2000m core= 2 cores
Memory: 1 Mi = 220 bytes
Disk: 1 MB = 106 bytes


# Prometheus Metrics
| Metrics Name  | Prometheus Query Language |
| ------------- | ------------- |
| CPU Usage (by namespace) | sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{namespace!= "prometheus", container!=""}) by (namespace) |
| CPU Usage (by pod) | sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{namespace="$yournamespace", container!=""}) by (pod)  |
| CPU Usage (by container) | sum(node_namespace_pod_container:container_cpu_usage_seconds_total:sum_irate{namespace="$yournamespace", container!=""}) by (pod,container) |
| Memory Usage (by namespace) | sum(container_memory_working_set_bytes{ namespace!= "prometheus", container!="", image!=""}) by (namespace) |
| Memory Usage (by pod) | sum(container_memory_working_set_bytes{namespace="$yournamespace",container!="", image!=""}) by (pod) |
| Memory Usage (by container) | sum(container_memory_working_set_bytes{namespace="$yournamespace",container!="", image!=""}) by (pod,container) |

# Prometheus Chart View
Observe the memory or CPU trend in certain period.
![image](https://user-images.githubusercontent.com/6374885/225497773-0b78bc0c-dd76-4228-9565-e7c5e8fd6821.png)  
![image](https://user-images.githubusercontent.com/6374885/225497802-00941a8b-e431-4b55-9681-492c8b7a1fde.png)

