![placeholder image](https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Kubernetes Networking - Networking Namespaces

## Introduction
This section deals with Kubernetes Networking.

## Notes about the Kubernetes Networking Namespaces

When a container is created, we create a network namespace for it so it has no visibility to the network interfaces on the host machine. The container network namespace has its own virtual network interface.

## CoreDNS in K8s

So how can we reach from one pod to another pod? We add an entry into the /etc/hosts file of one pod for the other pods that needs to reach. But this approach is not practical as there are 100 of pods created all the time.

So the solution is to add the ipaddresses to a common DNS server and point the pod to lookup in this server by adding an entry in the `/etc/resolve.conf` file with `nameserver <ip-address>`

Prior to K8s v1.12 - the DNS server was called `kube DNS` whereas after v1.12, it is called `Core DNS`.

CoreDNS is deployed as a deployment in the cluster with 2 replicas. This pod run Core DNS executable. When a CoreDNS pod is created, there is also a ClusterIP type service called `kube-dns` created, to make it accessible from other pods.
