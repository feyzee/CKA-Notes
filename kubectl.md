# kubectl
## commands
### imperative
`create deployment.yml` - deploys objects in the spec provided
`create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml` - generate [[deployment]] [[yaml]] file (-o yaml)
`create namespace dev` - creates a namespace dev
`create -f pod-deplyment.yml --namespace=dev` - creates a pod in [[namespaces]] dev
`create service clusterip redis-service --tcp=6379` - creates a service with clusterip and port set as 6379
`create --namespace=dev-ns deployment redis-deploy --image=redis --replicas=2` - create a deployment *redis-deploy* in namespace *dev-ns* with 2 replicas 
`config set-context $(kubectl config current-context) --namespace=dev` - switch namespace permanently to *dev*
`describe pod pod-name` - describes the pod's details
`edit pod nginx` - opens up an editor for editing the definition of the pod *nginx*
`expose deployment nginx --port 80` - expose port 80 for [[deployment]] *nginx*
`expose pod nginx --port=80` - expose port 80 to pod *nginx*
`get nodes` - list [[node]]
`get pods -A` - list all [[pods]] available
`get pods -o wide` - gives more info horizontally
`get pods --name=kube-system` - lists the pods inside the [[namespaces]] *kube-system*
`get pods -A --selector app=MyApp --no-headers | wc -l` - selects all the pods with specified [[labels & selectors|labels]]. `--no-headers` doesnt show header
`get get replicaset` - gets inform [[replicaset]]
`get svc` - list all [[services]] running
`replace -f deplyment.yml` - replaces current [[deployment]] 
`run nginx --image nginx:latest` - deploys nginx as a pod
`run nginx --image=nginx --dry-run=client -o yaml` - Generate POD Manifest [[yaml]] file (-o yaml)
`scale --replica=6 -f replicaset-definition.yml/replicaset my-app` - update the number of [[pods]] in the system
`set image deployment nginx nginx=nginx:alpine` - change image for the pod to *nginx:alpine* in the deployment *nginx*
`taint nodes node-name key=value:taint-effect`
`--dryrun=client -o yaml > pod.yml` - dumps the pod definition to a [[yaml]] file

### declarative
