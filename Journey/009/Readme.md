![placeholder image](https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Kubernetes Networking

## Introduction
This section deals with Kubernetes Networking.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Networking

### Handy commands

1. `ip link` - List and modify interfaces on the host.
2. `ip addr` - IP addresses assigned to those interfaces.
3. `ip addr add 192.168.1.10/24 dev eth0` - Set IP addresses on those interfaces.
4. `ip route` - To view routing table
5. `ip route add 192.168.1.0/24 via 192.168.2.1` - Add entries into the routing table.
