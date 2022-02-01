# kubelet
- it is main agent that runs on every worker nodes and registers the node with [[kube api server]]
- it recieves pod definitions from [[kube api server]]
- it interacts with [[container runtime engine]] to run associated containers with the pod
- it reports node and [[pods]] state to master [[node]] periodically
- kubelet must be manually deployed in the nodes when a cluster is brought up using [[kubeadm]]
- it runs as a daemon service