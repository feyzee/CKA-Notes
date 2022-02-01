# scheduler
- scheduler is responsible for deciding which pod goes to which node
      - it doesnt place the [[pods]] on the [[node]], that job is for [[kubelet]]
- kube scheduler watches for new workloads/pods and assigns them to a [[node]] based on several scheduling factors. these include
      - are there enough resources required for the pod
      - is the [[node]] healthy / capacity availability
      - are the network ports for pods available
      - [[node affinity]] and anti affinity rules
      - [[taints]] and [[tolerations]]
- scheduler assigns node to a pod by filltering out based on
      - resource requirements, this can include cpu/memory needed by the application running inside application
      - ranking of the pod based on the priority of 1 to 10
- `/etc/kubernetes/manifests/kube-scheduler.yml`
- a cluster can multiple schedulers same time
   - which scheduler to use can be instructed when a pod is created
   - when a new scheduler is created change the parameter `--scheduler-name` when launching it in the cluster 
- a custom scheduler if needed can be created as k8s is highly extensible.
   - this scheduler can be packages as default one if needed

## manual scheduling
- if no scheduler is present in the cluster, the state of the pods will be pending

### nodeName
- a `nodeName` object in the [[yaml]] definition for [[pods]] can be used to avoid the pending state and manually schedule to a [[node]]
- it is the simplest form of node selection constraint
- it is binding object that refers to name of the [[node]] the [[pods]] must be scheduled to
- by default it's set as empty, scheduler will auto pick a [[node]] and add this in config that stored by the kubernetes
- if the pod is already created the `nodeName` object can't be added by changing the [[yaml]] definition
- to change this, send a *POST* request of binding object to [[pods]] binding api
      - `curl --header 'Content-Type: application/json' --request POST --data '{"apiVersion": "v1", "kind":"Binding", "metadata":{"name":"nginx"},"spec":{"containers":[{"name":"nginx","image":"nginx"}],"nodeName":"kube-01"}}' https://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding`

## systemd service
### default scheduler
```sh
ExecStart=/usr/local/bin/kube-scheduler \\
   --config=/etc/kubernetes/manifests/kube-scheduler.yml
   --scheduler-name=default-scheduler
```

### custom scheduler
```sh
ExecStart=/usr/local/bin/custom-k8s-scheduler-binary \\
   --config=/etc/kubernetes/manifests/kube-custom-scheduler.yml
   --scheduler-name=kube-custom-scheduler
```

## kubeadm
### manifest
```yaml
apiVersion: v1
kind: Pod
metadata:
   name: kube-scheduler
   namespace: kube-system
spec:
   containers:
   - command:
      - kube-scheduler
      - --address=127.0.0.1
      - --kubeconfig=/etc/kubernetes/scheduler.conf
      - --leader-elect=true
      - --scheduler-name=kube-custom-scheduler
      - --lock-object-name=kube-custom-scheduler # used with leader-elect
      image: k8s.gcr.io/kube-scheduler-amd64:v1.11.3
      name: kube-scheduler
```