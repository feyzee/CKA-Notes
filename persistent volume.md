# persistent volume
- volume in a host machine is not recommended, use a third party storage driver like glusterfs or ebs

# definition
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
	name: pv
spec:
	accessModes:
	  - ReadOnlyMany
	  - ReadWriteOnce
	  - ReadWriteMany
	capacity:
		storage: 1 Gi
	hostPath:
		path: /tmp/data
	awsElasticBlockStore:
		volumeID: <volume-id>
		fsType: ext4
```