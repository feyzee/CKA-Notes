# taint
- taints are set on nodes
- taint allows to restrict which pods gets scheduled to which nodes
- taints and [[tolerations]] does not tell [[scheduler]] to schedule particular [[pods]] to the [[node]], instead it tells the [[scheduler]] it can only accept the pods with certain [[tolerations]]
      - to restrict a pod to certain [[node]], use [[node affinity]]
- there are three taint types available
      - `NoSchedule`
      - `PreferNoSchedule`
      - `NoExecute`
            - if this effect is applied to the [[node]], it will effective immediately evict all the existing [[pods]] without it's [[tolerations]] from the [[node]]
- when a [[cluster]] is created a taint is set on master node to disallow scheduling of worker pods
      - `kubectl describe node kubemaster | grep Taint`

## command
`taint nodes node-name key=value:taint-effect`