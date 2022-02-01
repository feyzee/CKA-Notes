# labels
- labels are properties attached to each object
- labels are specified in metadata section of [[yaml]] definition file
- labels are defined as a key value pair
- key can be anything and doesnt need to be defined beforehand
- no limits for labels

# selector
- selectors are used for specifying which and what type of pod to be filtered
- `--selector` paramater can be used with [[kubectl]] command
- selectors can be used for grouping [[pods]] when specifying [[replicaset]]
- for [[yaml]] definition selectors are specified in `selector` section

# annotations
#k8stodo 