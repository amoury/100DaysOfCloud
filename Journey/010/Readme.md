![placeholder image](https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Kubernetes Networking

## Introduction
This section deals with Kubernetes Networking.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Networking

How do 2 nodes / computers talk to each other? By using something called **switch**. We need an interface (eg. - eth0) on each host - physical or virtual. 
Using the command `ip link` you can check the list of interfaces on the host.

We use **`eth0`** to connect to the network. Let's say we want to connect to the network with IP address `192.168.1.0`, then we need to assign the system with the IP address in the same range by using the command `ip addr add 192.168.1.10/24 dev eth0`.

A switch can only enable communication within the devices connected on the same network.

How can a systemA (ip - `192.168.1.10`) reach the systemB (ip - `192.168.2.10`) which is on another network? This can be done through **router**. Since a router connects to 2 different networks, it gets 2 ips assigned (for eg - `192.168.1.1` and `192.168.2.1`)

To see the existing routing configuration on the system, run the command `route` - it displays the kernel's routing table. Gateway the ip from which a system can communicate with the system on any other network. So basically **gateway** is the ip of the router. If we don't explictly configure that, the system will only be able to communicate with other systems on its own network.

To configure the gateway, we can use the command `ip route add 192.168.2.10/24 via 192.168.1.1` where `192.168.1.1` is the ip of the router.

**NOTE** - `/24` is a CIDR notation. [Read this url for better understanding](https://networkengineering.stackexchange.com/a/3873).

So in this case, adding `/24` is like telling the computer that any address from `192.168.2.0` to `192.168.2.255` is part of the same network. If it was `/16` then it would mean that all the address from `192.168.0.0` to `192.168.255.255` belongs to the same network.

`ip route add default via 192.168.2.1` - This command will add a default gateway at `192.168.2.1`, so that traffic to any ip address which is not explicitly configured, can be redirected to the router.

In Linux, by default packets are not forwarded to another interface i.e. packets received on `eth0` will not be forwarded to `eth1` automatically. To enable forwarding from one interface to another, check the configuration in the file on path `cat /proc/sys/net/ipv4/ip_forward`. By default, the value is set to 0. Change it to 1 and save the file.


### DNS Resolution

- Instead of adding thousands of entries in the `/etc/hosts` file on all the different hosts in the network, we create a create DNS server and point the hosts to lookup in this DNS server.

Every host has a DNS resolution configuration file at `/etc/resolve.conf`. You make an entry into this file specifying the address of the DNS server.

Now everytime the host comes across a host name that it does not know about, it automatically reaches out to this DNS server.


### Handy commands

1. `ip link` - List and modify interfaces on the host.
2. `ip addr` - IP addresses assigned to those interfaces.
3. `ip addr add 192.168.1.10/24 dev eth0` - Set IP addresses on those interfaces.
4. `ip route` - To view routing table
5. `ip route add 192.168.1.0/24 via 192.168.2.1` - Add entries into the routing table.
