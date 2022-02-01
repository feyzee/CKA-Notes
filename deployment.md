# deployment
- when a new deployment is created a rollout is performed.
	- each rollout for same deployment is a revision
	- when next rollout is created it'll be revision 2 and so on..
	- this keeps tracks of deployments
	- allows for easy rollback if needed using revisions
- use [[kubectl]] to apply a yaml definition with changes to the deployment
	- a revision is auto created
- `kubectl set` command can be used to update the deployment imperatively 

## deployment strategy
- available strategies
	- recreate - takes down the entire deployment and redeploy with new updates
	- rolling - default strategy. takes down a pod with older version and brings up new pods, one by one to avoid downtime.

### rolling upgrades
- a [[replicaset]] is created with new pods and replaced one by one and the old replicaset is removed when the rollout is complete and vice versa for rollbacks.

# commands
`rollout status deployment/my-deployment` - shows the status of the deployment
`rollout history deployment/my-deployment` - shows the revisions/history of the deployment
`rollout undo deployment/my-deployment` - rollback the last deployment
`set image deployment/mydeployment nginx=nginx:1.9.1` - changes the image of the deployment imperatively

# definition
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```