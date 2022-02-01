# kube api server
- it is responsible for orchestrating all the operations within the [[cluster]]
- it is frontend to kubernetes [[control plane]]
- all external and internal communications go through [[kube api server]]
- it exposes restful api on port **443**
- it is used by external users to perform management operations on the [[cluster]]
- it is used by services to make necessary changes to the [[cluster]]
- it is used by worker nodes to communicate with the server
- also provides authentication and authorisation checks for secure connection
- [[kubectl]] command is used for communicating with [[kube api server]]
      - when a command is issued request is authenticated first and validated
- api server works with [[etcd]] to validate the state of the cluster
- if deployed using [[kubeadm]] api server is deployed as a pod in master node
- `/etc/kubernetes/manifests/kube-apiserver.yml`

## daemon service
`--authorization-mode=Node|RBAC`
`--client-ca-file=/path/to/certifcate.pem`
`--etcd-servers=https://127.0.0.01:2379`
`--etcd-cafile=/path/to/certifcate.pem`
`--etcd-certfile=/path/to/certifcate.pem`
`--etcd-keyfile=/path/to/certifcate.pem`
`--kubelet-certificate-authority=/path/to/certifcate.pem`
`--kubelet-client-certificate=/path/to/certifcate.pem`
`--kubelet-client-key=/path/to/certifcate.pem`
`--kubelet-https=true|false`

