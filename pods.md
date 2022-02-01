# pods
- a pod will have a main container which will represent the application
- containers inside a pod communicate each other via `localhost` and the ports they expose
- a pod will have a unique ip address that other pods can use for communications
- pod also contains: #k8stodo 
      - init container
      - sidecar containers
      - volumes
      - helper containers
- when a pod dies/or is destroyed other objects in container are also destroyed automatically
- port of the pod running on the node is known as target port
      - if it isnt specified port of the [[services|targetport]] is used 
- `command` and `args` options in the definition file allows us to change the command to execute and it's arguments provided by the container/image
	- `command` and `args` fields are equivalent to [[entrypoint]] and `cmd` fields in Dockerfile respectively
- [[environment variables]] can be set using `env` property.
	- it is an array.
	- [[configmaps]] and [[secrets]] can be set as values.

## pod creation
- when a request comes in for a new pod, [[kube api server]] creates a new entry for a pod in [[etcd]]
- [[scheduler]] monitoring the situation, assigns the pod to a [[node]] and updates the [[kube api server]] which updates the [[etcd]]
- [[kube api server]] then sends a request to [[kubelet]] on the appropriate [[node]]
- [[kubelet]] then creates the pod and instructs the application runtime engine([[docker]] or [[containerd]]) to deploy the pod
- after the pod is deployed [[kubelet]] updates the status to [[kube api server]] which in turn updates [[etcd]]

## init container
## sidecar containers
## volumes
## helper containers

# commands

# definition
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
	      command: ["nginx"]
		  args: [""]
		  env:
			  - name: COLOR1
				value: red
			  - name: COLOR2
				valueFrom:
					configMapRef:
						name: app-config
						key: COLOR2
			  - name: COLOR3
				valueFrom:
					secretKeyRef:
		  envFrom:
			  - configMapRef:
					name: app-config
			  - secretRef:
					name: root-pw
```