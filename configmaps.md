# configmaps
- configmaps are used to pass configuration data in form of key value pairs.
- when a [[pods|pod]] is created configmaps can be used to inject key value pairs as [[environment variables]]

# command
`create configmap app-config --from-literal=COLOR1=red` - here `app-config` is the configuration name
`create configmap app-config --from-fil=config.ini` - here config is read from an input file

# definition
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
	name: app-config
data:
	COLOR1: red
	COLOR2: blue
	COLOR3: green
