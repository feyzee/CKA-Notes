# authorization
- following are list of authorization methods supported by kubernetes
	- Node
	- ABAC
	- [[RBAC]]
	- Webhooks
	- Always allow
	- Always deny
- modes are set in [[kube api server]] service file parameter `--authorization-mode`
	- multiple options can be specified

# commands
`auth can-i create deployments` - to check whether user has permission to create deployments
`auth can-i create pods --as dev-user` - to check whether user has permission to create pods as *dev-user*

