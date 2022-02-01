# loadbalancer
-

# definition
```yaml
apiVersion: v1
kind: Service
metadata:
      name: my-app-service
spec:
      type: LoadBalancer
      ports:
            - targetPort: 80 # port of the pod
              port: 80 # port of the service
```