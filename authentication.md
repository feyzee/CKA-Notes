# authentication
connection to k8s cluster can be authenticated using the following options
- static text file with username and password
- static tokens
- certificates
- identity services like ldap & ad

### static text file with username and password
- if cluster is set up using [[kubeadm]] then the above parameter needs to be specified in the definition file for [[kube api server]]
- to connect using curl use the following
	- `curl -v -k https://cluster-address.k8s:6443/api/v1/pods -u "user1:password1"` 
- not recommended as it's not secure enough
- volume mounts can be used to share the file
- passwd using the parameter `--basic-auth-file=file.csv` when [[kube api server]] is invoked or in the service config

### static tokens
- this works similiar to the above method. same parameter needs to specified. here instead of password specifiy token.
- to connect using curl use the following
	- `curl -v -k https://cluster-address.k8s:6443/api/v1/pods --header "Authorization: Bearer cGFzc3dvcmQx"` 
- not recommended as it's not secure enough
- `system` keyword must be be prefixed for the following kubernetes services as they are system services

### certificates
[[certificates]]

### identity services like ldap & ad



Edit the kube-apiserver static pod configured by kubeadm to pass in the user details. The file is located at `/etc/kubernetes/manifests/kube-apiserver.yaml`

1.  apiVersion: v1
2.  kind: Pod
3.  metadata:
4.   name: kube-apiserver
5.   namespace: kube-system
6.  spec:
7.   containers:
8.   - command:
9.   - kube-apiserver
10.   <content-hidden>
11.   image: k8s.gcr.io/kube-apiserver-amd64:v1.11.3
12.   name: kube-apiserver
13.   volumeMounts:
14.   - mountPath: /tmp/users
15.   name: usr-details
16.   readOnly: true
17.   volumes:
18.   - hostPath:
19.   path: /tmp/users
20.   type: DirectoryOrCreate
21.   name: usr-details

Modify the kube-apiserver startup options to include the basic-auth file

1.  apiVersion: v1
2.  kind: Pod
3.  metadata:
4.   creationTimestamp: null
5.   name: kube-apiserver
6.   namespace: kube-system
7.  spec:
8.   containers:
9.   - command:
10.   - kube-apiserver
11.   - --authorization-mode=Node,RBAC
12.   <content-hidden>
13.   - --basic-auth-file=/tmp/users/user-details.csv

Create the necessary roles and role bindings for these users:

  

1.  ---
2.  kind: Role
3.  apiVersion: rbac.authorization.k8s.io/v1
4.  metadata:
5.   namespace: default
6.   name: pod-reader
7.  rules:
8.  - apiGroups: [""] # "" indicates the core API group
9.   resources: ["pods"]
10.   verbs: ["get", "watch", "list"]

12.  ---
13.  # This role binding allows "jane" to read pods in the "default" namespace.
14.  kind: RoleBinding
15.  apiVersion: rbac.authorization.k8s.io/v1
16.  metadata:
17.   name: read-pods
18.   namespace: default
19.  subjects:
20.  - kind: User
21.   name: user1 # Name is case sensitive
22.   apiGroup: rbac.authorization.k8s.io
23.  roleRef:
24.   kind: Role #this must be Role or ClusterRole
25.   name: pod-reader # this must match the name of the Role or ClusterRole you wish to bind to
26.   apiGroup: rbac.authorization.k8s.io

Once created, you may authenticate into the kube-api server using the users credentials

`curl -v -k https://localhost:6443/api/v1/pods -u "user1:password123"`