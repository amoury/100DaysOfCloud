![placeholder image](https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1200&q=80)

# Kubernetes Cluster Maintenance

## Introduction
Knowing how to properly backup your running pods and take down nodes for upgrades is important for an administrator.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Architecture

There are 2 types of pods in the clusters - the ones that are created by a deployment and the stand alone ones. By default, if the pod is created by a deployment, the **ReplicationController** watches the cluster to maintain the desired number of pods. If a pod goes down, then ReplicationController tries to bring up another instance of the pod.

With that in mind, a node may have some pods that are created by a deployment and some standalone ones. If you need to take down a node for some upgrades or maintenance and you directly take it down, the master node's control plane waits for **5 mins** by default, then emits the signal that the pod is dead. At this point ReplicationController tries to bring up another pod on the next available node. 

But if the pod is a standalone pod, it is then lost forever - thus disrupting the services for good.

To avoid the disruption either for 5 mins or forever, you first drain the pod. Draining the pod will make sure that the pod on current node is first replaced by another pod on a different node. If there are pods that are not created by the deployment, then it will first give the warning and will continue with draining only if you force it to.

The command is `kubectl drain <node-name>`


**cordoning** 

`kubectl cordon NODE` - Mark node as unschedulable.
