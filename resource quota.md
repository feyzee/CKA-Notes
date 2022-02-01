# resource quota

## yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
      name: "hello"
      namespace: dev
      label:
            type: backend
            app: myapp
spec:
      containers:
            - name: nginx-server
              image: nginx:latest
        hard:
            pods: 10
            requests.cpu: 4
            requests.memory: 5Gi
            limits.cpu: 10
            limits.memory: 10Gi
```