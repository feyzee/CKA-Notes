# container runtime engine
- a container runtime allows running container images defined by the pod. it also pulls the images from a registry.
- it is responsible and managing for running containers
- it abstracts container management for kubernetes
- there is container runtime interface which is  an interface for third party container runtimes
- containerd is default container runtime for k8s
      - docker has been depreciated