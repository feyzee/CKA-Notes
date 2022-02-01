# replicaset
- replicaset can also manage pods that aren't part of the replicaset when they were creation
- it monitors pods constantly to check if there's any change in it's state 
- the [[labels & selectors#labels|labels]] are specified in the template section for [[labels & selectors#selector|selectors]] to group them

# definition
```yaml
---
# equality based selector
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
---
# set based selector
apiVersion: v1
kind: Service
metadata:
      name: my-app-service
spec:
      selector:
            matchExpressions:
                  - { key: tier, operator: In, values: [frontend] }
            matchLabels:
                  env: prod
      replicas: 3
      template:
            metadata:
                  name: myapp
                  labels:
                        app: myapp
      spec:
            containers:
                - name: myapp
                  image: myapp:latest
                  ports:
                      - containerPort: 80
```