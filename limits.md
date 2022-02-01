# resource requests
- k8s will intelligently schedule to nodes based on the resource requirements
- by default the cpu and memory are limited to `1` and `512Mi` respectively. ^24a178
- if no [[node]] with sufficient resources are available, [[pods]] will be pending state
- cpu values can be as low as `0.1` or `1m` (m stands for milli)
- `1` count equals to 1 vCPU in AWS or 1 core in GCP and Azure or 1 Hyperthread
- memory is denoted in either G/M/K (1000) or Gi/Mi/Ki (1024). 
- `limits` section in pod definition can be used set new [[#^24a178|default limits]]
- for the pod to pick up those defaults you must have first set those as default values for request and limit by creating a `LimitRange` in that namespace. 
## definition
```yaml
---
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
 resources:
   limits:
    - default:
       memory: "512Mi"
      defaultRequest:
       memory: "256Mi"
      type: Container
---
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-limit-range
spec:
 resources:
   limits:
    - default:
       cpu: 1
      defaultRequest:
       cpu: 0.5
      type: Container
```