# kubeconfig
- located at `$HOME/.kube/config`

# commands
- `config view --kubeconfig=$HOME/.kube/config`
- `config use-context admin-playground@k8s-playground`

# definition
```yaml
apiVersion: v1
kind: Config
current-context: admin-playground@k8s-playground
clusters:
	- name: k8s-playground
	  cluster:
		  certificate-authority: "~/certificates/ca.crt"
		  server: "https://k8s.playground:6443/"
contexts:
	- name: admin-playground@k8s-playground
	  context:
		  cluster: k8s-playground
		  user: admin-playground
		  namespace: backend
users:
	- name: admin-playground
	  user:
		  client-certificate: admin.crt
		  client-key: admin.key
```