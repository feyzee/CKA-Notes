# YAML
yaml is used by kubernetes for specifying deployments

# definition
various things in a kubernetes yaml definition

`apiVersion` - kubernetes api version.
`kind` - type of object to be created
`metadata` - data about the object. it's a dict. defines name, labels etc.
`spec` - defines the object

## kind/apiVersion values
| kind       | apiVersion |
| ---------- | ---------- |
| POD        | v1         |
| Service    | v1         |
| ReplicaSet | apps/v1    |
| Deployment | apps/v1    |
| Namespace  | v1         | 

## various options
[[resource quota]]