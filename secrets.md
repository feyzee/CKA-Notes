# secrets
- secrets are used to values that needs to be secured.
- a secret is only sent to a node if a pod on that node requires it. 
- secrets are not encrypted
- [[kubelet]] stores the secret into a tmpfs so that the secret is not written to disk storage. 
- once the Pod that depends on the secret is deleted, kubelet will delete its local copy of the secret data as well.

# command
`create secret generic root-pw --from-literal=PASSWD=password`
`create secret generic root-pw --from-file=~/hello.pwd`
`get secret root-pw -o yaml`

# definition
```yaml
apiVersion: v1
kind: Secret
metadata:
      name: root-pw
data:
	PASSWD: password
	SEC_PASSWD: cGFzc3dvcmQ=
```