# cluster store
- it stores all configurations and state of the entire cluster
- **etcd** is a key value data store used in k8s as default cluster store
- it acts as single source of truth
- when a deployment is done using [[kubectl]], the configuration is stored in cluster store

# etcd
- by default **etcd** listens on port 2379
- it stores data for
      - minions
      - nodes
      - [[pods]]
      - configs
      - [[secrets]]
      - accounts
      - roles
      - bindings
- [[kubeadm]] deploys **etcd** as a pod in kube system namespace

## etcdctl
- it is a cli tool for interacting with **etcd**
      - `--advertise-client-urls` parameter is used in **etcdctl** to make it listen to specific address/port
      - `--intial-cluster` is where you specify different instances of **etcd** service
- it supports two API versions - v2 & v3
      - switch between by setting an environment variable - `export ETCDCTL_API=3`
- when API version is not set, it is assumed to be set to version 2.
- and version 3 commands listed above don't work.
- when API version is set to version 3, version 2 commands listed above don't work.
- path to certificate files must be specified for authentication to **etcd**
- the certificate files are available in the etcd-master at the following path -
      - `--cacert /etc/kubernetes/pki/etcd/ca.crt`     
     - `--cert /etc/kubernetes/pki/etcd/server.crt`     
    - `--key /etc/kubernetes/pki/etcd/server.key`

# backups
- when taking backup [[kube api server]] needs to be stopped
- when running backup commands following parameters must be provided
	- `--cacert` ca certificate
	- `--cert` etcd server certificate
	- `--endpoints` endpoints address
	- `--key` key file

# commands
### version 2
`set key value` - create/set a key and value for it
`get key` - get the value of a key
`backup`
`cluster-health`
`mk`
`mkdir`
### version 3
`get`
`put`
`snapshot save` 
`endpoint health`

    kubectl exec etcd-master -n kube-system -- && \
      sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 && \
      --cacert /etc/kubernetes/pki/etcd/ca.crt --cert && \ /etc/kubernetes/pki/etcd/server.crt  --key &&\ /etc/kubernetes/pki/etcd/server.key" &&
