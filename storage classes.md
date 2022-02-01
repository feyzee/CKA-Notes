# storage classes
- storage classes allows for dynamically provisioning/creating volumes using a provisioner defined.
	- if AWS EBS is used as a provisioner, when creating new [[persistent volume]], it will automatically create new volumes in EBS.
	- it will attach the newly created [[persistent volume]] to the [[pods]] when the [[persistent volume claims]] is made by it.

# definition
For GCP volumes
```yaml
api: storage.k8s.io/v1
kind: StorageClass
metadata:
	name: google-storage
provisioner: kubernetes.io/gce-pd
```