# services
- kubernetes services enables communication between various components within and outside of the application
- it allows to establish connectivity between outside data sources
- if there are multiple pods with same labels, the service will automatically route the traffic to all of the them
      - algorithm for routing is random
      - and sessionaffinity is set as yes
- a service can span multiple nodes
      - the ip address will differ for different [[node|nodes]] but [[nodeport|port]] remains same 
- if pods are removed or added it'll automatically update itself for routing

## types of services
[[nodeport]]
[[clusterip]]
[[loadbalancer]]

# definition
```yaml
apiVersion: v1
kind: Service
metadata:
      name: my-app-service
      namespace: dev
spec:
      type: NordPort
      ports:
            - targetPort: 80 # port of the pod
              port: 80 # port of the service
              nodePort: 30008 # port of the node
      selector:
            app: myapp # labels
            type: frontend
```