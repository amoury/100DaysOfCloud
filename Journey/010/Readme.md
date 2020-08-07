![placeholder image](https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Kubernetes Networking

## Introduction
This section deals with Kubernetes Networking.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Networking

How do 2 nodes / computers talk to each other? By using something called **switch**. We need an interface (eg. - eth0) on each host - physical or virtual. 
Using the command `ip link` you can check the list of interfaces on the host.

We use **`eth0`** to connect to the network. Let's say we want to connect to the network with IP address `192.168.1.0`, then we need to assign the system with the IP address of same network by using the command `ip addr add 192.168.1.10/24 dev eth0`.

A switch can only enable communication within the devices connected on the same network.

How can a systemA (ip - `192.168.1.10`) reach the systemB (ip - `192.168.2.10`) which is on another network? This can be done through **router**. Since a router connects to 2 different networks, it gets 2 ips assigned.

### Handy commands

1. `ip link` - List and modify interfaces on the host.
2. `ip addr` - IP addresses assigned to those interfaces.
3. `ip addr add 192.168.1.10/24 dev eth0` - Set IP addresses on those interfaces.
4. `ip route` - To view routing table
5. `ip route add 192.168.1.0/24 via 192.168.2.1` - Add entries into the routing table.
