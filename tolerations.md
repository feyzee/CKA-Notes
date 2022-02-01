# tolerations
- tolerations are set on pods
- tolerations are added to pods to avail the taint feature of k8s.
- if a toleration is added to a pod, it can be [[scheduler|scheduled]] to the tainted nodes with same key value pair

## definition
```yaml
tolerations:
- key: "app"
  value: "blue"
  operator: "Equal"
  effect: "NoSchedule"
```