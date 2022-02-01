# persistent volume claims
- `persistentVolumeReclaimPolicy` is used to specify whether the volume needs to deleted or not after the pods is destroyed
	- options available are
		- `Retain`
		- `Delete`
		- `Recycle` - deletes the data and makes it available for other pv claims

# definition
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
	name: pv-claim
spec:
	accessModes:
	  - ReadWriteOnce
	resources:
		requests:
			storage: 500 Mi
	hostPath:
		path: /tmp/data
	storageClassName: google-storage
	awsElasticBlockStore:
		volumeID: <volume-id>
		fsType: ext4
```
