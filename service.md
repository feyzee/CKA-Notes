# service
- a service is used for communicating with a pod. when a service is created for a pod it auto assigns an ip address that other [[pods]] can use for communication
- a service is not bound to node, it is available cluster-wide.
	- this service is called a [[clusterip]]
- a service that's available to public internet, and not limited to the cluster is called a [[nodeport]]
	- the ip address is assigned to the node where pod belongs to 
- if used in a cloud environment, [[loadbalancer]] type is available.
	- when an object of kind [[loadbalancer]] is created kubernetes asks the cloud provider for setting a load balancer in their environment