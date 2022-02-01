# network policies
- not all netowkring solutions in k8s supports network policies

# definition
```yaml
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
	name: db-policy
spec:
	podSelector:
		matchLabels:
			role: db
	policyTypes:
	  - Ingress
	  - Egress
	ingress:
	  - from:
		  - podSelector:
				matchLabels:
					name: api-pod
		    namespaceSelector:
				matchLabels:
					name: prod
		  - ipBlock:
			    cidr: 192.168.5.10/32
		ports:
		  - protocol: TCP
				port: 3306
	egress:
	  - to:
		  - podSelector:
				matchLabels:
					name: db-pod
		  - ipBlock:
			    cidr: 192.168.5.12/32
		ports:
			protocol: TCP
			port: 80
```

```yaml
kind: NetworkPolicy
metadata:
  name: internal-policy
spec:
  podSelector:
    matchLabels:
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  egress:
  - to:
    - podSelector:
        matchLabels:
            name: payroll
    ports:
    - protocol: TCP
      port: 3306
 - to:
    - podSelector:
        matchLabels:
            name: mysql
   ports:
    - protocol: TCP
      port: 8080
 - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP
```