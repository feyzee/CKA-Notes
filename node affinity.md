# node affinity
- available types of affinity
      - `requiredDuringSchedulingIgnoredDuringExecution`
      - `preferredDuringSchedulingIgnoredDuringExecution`
      - `requiredDuringSchedulingRequiredDuringExecution`

|        | DuringScheduling | DuringExecution | Comment                                                                                                                                                                         |
| ------ | ---------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Type 1 | Required         | Ignored         | If the labels arent found during scheduling, pod is not created. If labels are removed during execution pod isnt evicted from the node.                                         |
| Type 2 | Preferred        | Ignored         | If the labels are found will be scheduled to one of the matching nodes, else to any of the random nodes. If labels are removed during execution pod isnt evicted from the node. |
| Type 3 | Required         | Required        | If the labels arent found during scheduling, pod is not created. If labels are removed during execution pod is evicted from the node. Will be available in future release.      |

## definition
```yaml
spec:
      containers:
            - name: nginx
              image: nginx
      affinity:
            requiredDuringSchedulingIgnoredDuringExecution:
                  nodeSelectorTerms:
                        - matchExpressions:
                              - key: size
                                operator: In|NotIn|Exists
                                values:
                                    - Large
                                    - Small
```