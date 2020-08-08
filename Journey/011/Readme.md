![placeholder image](https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Kubernetes Networking - Networking Namespaces

## Introduction
This section deals with Kubernetes Networking.

## Notes about the Kubernetes Networking Namespaces

When a container is created, we create a network namespace for it so it has no visibility to the network interfaces on the host machine. The container network namespace has its own virtual network interface.

### To create network namespace - 

`ip nets add <namespace-name>`

`ip netns exec <namespace-name> ip link` - command to list the interfaces within the namespace from the host OR
`ip -n <namespace-name> link` - Same as above, just simpler


To establish the network between the 2 namespaces - 

1. Create a virtual cable or pipe with the command `ip link add veth-red type veth peer name veth-blue`. Here **veth-red** and **veth-blue** are the names of the two ends of the pipe.

`ip link add veth-red type veth peer name veth-blue`

2. Now we attach the `veth-red` end to red namespace and we will have to do the same from `veth-blue`. We can do this by using the commands -

`ip link set veth-red netns red`

`ip link set veth-blue netns blue`

3. We then assign the ip address to each of these namespaces using the usual commands -

`ip -n red addr add 192.168.15.1 dev veth-red`
`ip -n blue addr add 192.168.15.2 dev veth-blue`

4. We then bring up the links using the commands -

`ip -n red link set veth-red up`
`ip -n blue link set veth-blue up`

5. For testing we can now ping from the red namespace to the blue's ip =

`ip netns exec red ping 192.168.15.2` 



In the cases when you have lot of namespaces and you want all of them to communicate with each other, you have to create all of them with a switch. And since connecting between namespace is a virtual network, we need to add virtual switch.
For this, there are some third party solutions available such as Linux Bridge, Open vSwitch, etc.

### Linux Bridge

To add the linux bridge to the network, we can use the command - 

`ip link add v-net-0 type bridge` 

Its currently down, so to bring it up, use the command -
`ip link set dev v-net-0 up`


The bridge acts as an interface for the host and as a switch for the namespaces.

To delete the virtual cable we created previously, use the command - 
`ip -n red link del veth-red`.

When you delete one end of the cable, the other end is deleted automatically.


To connect our `red` namespace to the bridge, we simply create the virtual cable similar to how we did previously  -

`ip link add veth-red type veth peer name veth-red-br`

Firstly, to attach `veth-red` end to the **red** namespace, use the command - `ip link set veth-red netns red`. Then to attach the `veth-red-br` end to the bridge, use the command `ip link set veth-red-br master v-net-0`

Now, assign the ip address to the namespace - `ip -n red addr add 192.168.15.1 dev veth-red` and then tuen it up `ip -n red link set veth-red up`


Since our bridge is just an interface on the host, we can assign it an ip address `ip addr add 192.168.15.5/24 dev v-net-0`. Now we can ping this network of namspaces from the host 



