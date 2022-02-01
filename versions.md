# versions
- api compatilble and supported with upto 3 minor versions
- specific versions of external tools used by k8s(etcd etc.) might required
- other core services used by k8s shouldn't be one version higher than [[kube api server]]
	- [[controller manager]] and [[scheduler|kube scheduler]] can be one version lower
	- [[kubelet]] and [[kube proxy]] can be two versions lower 
	- [[kubectl]] can be one version lower or higher
# command
- `get nodes` - will display the version of the node