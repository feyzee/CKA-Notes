# node
## upgrades
- `drain` command can be used to remove the pods from a node gracefully. this is useful if node needs to be shutdown for upgrade
- `uncordon` command is used to the cluster the node is available for scheduling the pods.
	- this step must be performed to enable scheduling of the pods to the node after the `drain` command
	- pods are not auto restored when `uncordon` is used on a node. cluster will only schedule newly created pods in the node .
- `cordon` - marks a node as unschedulable for the pods. this doesnt remove the existing pods from the node like `drain` 