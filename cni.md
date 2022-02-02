# container network interface
- spec for implementing the networking part for containers and it's orchestrators
- spec is implemented by a program called plugin. eg- weave, flannel, calico etc.
- following are responsibilities of container runtime
	- container runtime must create [[network namespace]]
	- identify the network container must attach to
	- container runtime to invoke Network Plugin (bridge) when container is added.
	- container runtime to invoke Network Plugin (bridge) when container is deleted.
	- config should be in JSON format
- following are responsibilities of plugins
	- must support commandline arguments DEL/ADD/CHECK
	- must support parameters for container id, network ns etc
	- must manage ip address assignment for [[pods]] 
	- must return results in a specific format
- CNI has support for plugins by default
	- bridge
	- vlan
	- ipvlan
	- macvlan
	- windows
	- IPAM plugins like
		- host-local
		- DHCP

# config
```JSON
{
	"cniVersion": "0.2.0",
	"name": "mynet",
	"type": "bridge",
	"bridge": "cni0",
	"isGateway": true,
	"ipMasq": true,
	"ipam": {
		"type": "host-local",
		"subnet": "10.22.0.0/16",
		"route": [
			"dst": "0.0.0.0/0"
		]
	}
}
```