# node controller
- it handles status of the nodes and take necessary actions to keep application running
- it is also responsible for onboarding new nodes to clusters
- it monitors the nodes continously every 5 second and if it stops receiving heartbeat it'll mark as unreachable
- if the [[node]] is still unreachable in the 40 second grace period then it'll mark it as unreachable 
- if the [[node]] is still not back up in the 5 minute pod eviction timeout the [[pods]] in the nodes are moved to other healthy [[node]] if they are part of a [[replicaset]]
- the timeout values can be set in the kube [[controller manager]] daemon service