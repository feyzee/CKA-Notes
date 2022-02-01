# node selector
- node selectors allows to place a pod in specific nodes
- labels and selectors are used to identify and place the pods on right nodes

## definition
```yaml
spec:
      containers:
            - name: nginx
              image: nginx
      nodeSelector:
              size: Large
```

`kubectl label nodes node01 size=m5xlarge`