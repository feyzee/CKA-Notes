# ingress
- ingress is similiar to layer 7 load balancer built into the cluster
- an ingress controller allows access to ingress resources. example include nginx, haproxy etc.
- ingress resources are deployed using k8s definition files

# definition
nginx ingress controller deployment
```yaml
apiVersion: networking.k8s.io/v1
kind: Deployment
metadata:
	name: nginx-ingress-controller
spec:
	replicas: 1
	selector:
		matchLabels:
			name: nginx-ingress
	template:
		metadata:
			labels:
				name: nginx-ingress
		spec:
		  - name: nginx-ingress-controller
			image: "quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.21.0"
		args:
			- '/nginx-ingress-controller'
			- --configmap=$(POD_NAMESPACE)/nginx-configuration
		env:
		  - name: POD_NAME
		    valueFrom:
				fieldRef: 
					fieldPath: metadata.name
		  - name: POD_NAMESPACE
		    valueFrom:
				fieldRef: 
					fieldPath: metadata.namespace
	ports:
		- name: http
		  containerPort: 80
		- name: https
		  containerPort: 443
```

nginx ingress service
```yaml
apiVersion: v1
kind: Service
metadata:
	name: nginx-ingress
spec:
	type: nodePort
	ports:
		- name: http
		  port: 80
		  targetPort: 80
		  protocol: TCP
		- name: https
		  port: 443
		  targetPort: 443
		  protocol: TCP
	selector:
		name: nginx-ingress
```

nginx resource for a single service
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
	name: ingress-single
spec:
	backend:
		serviceName: single-service
		servicePort: 80
```

nginx resource rules
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
	name: ingress-home-path
spec:
	rules:
	  - host: my-website.com
	    http:
		  paths:
		    - path: /
		      pathType: Prefix
			  backend:
				service:
					name: home-service
					port:
						number: 80
	  - host: admin.my-website.com
	    http:
		  paths:
			- path: /admin
		      pathType: Prefix
			  backend:
				service:
					name: admin-service
					port:
						number: 80
```