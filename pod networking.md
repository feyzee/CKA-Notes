# pod networking
- kubernetes doesnt implement networking for pod and expects user to set up the solution
- kubernetes has certain expectations for the networking solution
	- every [[pods]] should have an ip address
	- every [[pods]] should be able to communicate with every other [[pods]] in the same [[node]]
	- every [[pods]] should be able to communicate with every other [[pods]] on other nodes without NAT
