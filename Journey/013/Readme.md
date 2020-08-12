![placeholder image](https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2250&q=80)

# Kubernetes Networking - Networking Namespaces

## Introduction
This section deals with Kubernetes Networking.

## Notes about the Kubernetes Networking Namespaces

When a container is created, we create a network namespace for it so it has no visibility to the network interfaces on the host machine. The container network namespace has its own virtual network interface.

## DNS in K8s

Each node in the cluster has a node name and an ip address assigned to them.
- K8s deploys a built in DNS server within the cluster when you set it up. Whenever a service is created to expose any of the pods, a record is created within the Kube DNS server. It maps the service name to the IP address.

So we can reach out to the pod using the service name - `curl http://web-service`

### What happens when the service is located in a different Namespace - 

Let's say our `web-service` is located in the namespace **apps** then to reach that service we would have to reach out to `curl http://web-service.apps`. Below is the kube DNS table and this is how it resolves any service 

<img width="598" alt="Screen Shot 2020-08-12 at 5 41 20 AM" src="https://user-images.githubusercontent.com/16633104/89965736-8aaf4400-dc5e-11ea-9bea-e443641bc418.png">


