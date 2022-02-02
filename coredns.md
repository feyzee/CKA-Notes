# coredns
- dns server used by k8s insce v1.12+
- confid is stored in `/etc/coredns/Corefile`
- coredns

# config
```Corefile
.:53 {
	errors
	health
	kubernetes cluster.local in-addr.arpa ip6.arpa {
		pods insecure
		upstream
		fallthrough in-addr.arpa ip6.arpa
	}
	prometheus :9153
	proxy . /etc/resolv.conf
	cache 30
	reload
}
```