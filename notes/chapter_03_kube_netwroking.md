### What are the kubernetes networking requiremnt?
The network needs to satisfy the following (kubernetes) requirements:
1. All containers can communication with all other containers without NAT.
2. All nodes can communicate with all containers (and vice versa) withour NAT.
3. The IP that a container sees itself as is the same IP that others see it as.

### What are the four distinct networking problem?
1. Container to Container networking
2. Pod to Pod netwroking
3. Pod to service networking
4. Internet to service netwroking


to work our way from nothing to a(flannel style) overlay network in 4 "easy" steps
Step 1 : Single network namespace.
- Creating the name space
sudo ip netns add SCON

- Creating veth pair
sudo ip link add veth1 type with peer name veth2

- Adding one end of veth pair to namespace
sudo ip link set veth2 netns SCON

- Configuring the interface in the network namespace with an IP address
sudo ip netns exec 
- Enabling the interface on the node
- setting the loopback interface in thenetwork namespace.
- Setting the routes on the node
- Setting the default route in the network namespaces.


step 2 : Single node, 2 network namespaces.
step 3 : Multiple nodes, same L2 network.
step 4 : Multiple nodes, overlay network.