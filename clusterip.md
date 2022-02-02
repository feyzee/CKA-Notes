# clusterip
- ip address of a [[service]] limited to a cluster is known as [[clusterip]] 
- each group of pods will a single service interface for communicating effectively to access them

# definition
```yaml
apiVersion: v1
kind: Service
metadata:
      name: my-app-service
spec:
      type: ClusterIP # default type of the type
      ports:
          - targetPort: 80 # port of the pod
            port: 80 # port of the service
      selector:
            app: myapp # labels
            type: backend
```