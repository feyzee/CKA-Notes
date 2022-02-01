# kube proxy
- it is responsble for local cluster networking
- it makes sure each node gets its own ip address
- it is also responsible for routing networked traffic to load balanced services
- services for different pods can be assigned to access them
- it is deployed as [[daemonset]] by kubeadm