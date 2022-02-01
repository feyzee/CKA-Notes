# namespace
- kubernetes creates three namespaces by default
      - kube-system
            - contains resources related to core kubernetes services
      - kube-public
      - default
- namespaces are used for isolation between resources
- we can use different namespaces for isolating dev and prod environments
- each namespace can have different [[resource quota]] for the resources it can use(like nodes)
- services in the same namespace can use their name to access them
- services outside the namespace will have to append the namespace' name with name of the resource

`db-service.dev.svc.cluster.local`
- `db-service` is the service' name
- `dev` is the namespace
- `svc` refers to service
- `cluster.local` refers to dns domain

