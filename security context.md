# security context
- capabilities are limited to container level

# definition
```yaml
apiVersion: v1
kind: Pod
metadata:
	name: "hello"
spec:
	securityContext: # pod level
		runAsUser: 1000
    containers:
        - name: nginx-server
	      image: nginx:latest
	      command: ["nginx"]
		  args: [""]
		  securityContext: # container level
			runAsUser: 1000
			capabilities:
				add: ["MAC_ADMIN"]
```