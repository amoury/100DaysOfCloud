**Add a cover photo like:**
![placeholder image](https://unsplash.com/photos/hHntcuiLbOg)

# New post title here

## Introduction

Having a deeper understanding of the Kubernetes Architecture is important especially if you are aiming for a job as a DevOps Engineer or you are planning to appear for CKA exam i.e. Certified Kubernetes Administrator. 

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Architecture

`Nodes` are the most primary components of Kubernetes. So what is a Node? Node is simply a virtual or a physical machine / computer. Primarily there are two type of nodes in a cluster - **Master** node and a **Worker** node. The difference between a Master and a Worker node is the components installed on each node. 

In a typical cluster, there is one Master node and multiple Worker nodes. Master node contains control plane components - 

1. **Kube-apiserver** - Orchestrates all operations within the cluster. If Master node is the brain of the cluster, kube-apiserver is the left half of the brain.
2. **ETCD** - key-value store
3. **Controllers** - 
    - Node-Controller - Monitors nodes
    - Replication-Controller - Monitor pods and makes sure the desired number of pods are always up and running.
4. **Kube-scheduler** - Decides which containers / pods goes on which node (ship)


All nodes have following components -

1. **Container-runtime** - Popular one is Docker
2. **Kubelet** - Sending reports, liasing with master, managing the whole node. Listens to instructions from api-server and creates or destroys containers.
3. **Kube-proxy** - Monitors the rules configured and allows containers to communicate with each other

