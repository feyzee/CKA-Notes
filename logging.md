# metrics server
- metrics server is used for logging, monitoring and collecting metrics from the cluster
- each cluster can have one metrics server
- it is in memory solution and does not store on the disk
- [[kubelet]] contains a sub component called *cAdviser*
   - it is responsible for retrieving performance metrics from [[pods]] and exposing them to metrics server via kubelet api
- collects resource metrics from Kubelets and exposes them in Kubernetes apiserver through Metrics API for use by Horizontal Pod Autoscaler and Vertical Pod Autoscaler.
- Metrics API can also be accessed by `kubectl top`, making it easier to debug autoscaling pipelines.
- Metrics Server is not meant for non-autoscaling purposes