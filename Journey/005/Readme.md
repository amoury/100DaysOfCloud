![placeholder image](https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1200&q=80)

# Kubernetes Cluster Maintenance

## Introduction
Knowing how to properly backup your running pods and take down nodes for upgrades is important for an administrator.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Architecture

Kubernetes software releases follow **semver** to add versioning.

**kube-apiserver** - Has to be the latest version and the other components of the control plane cannot be higher than this. eg - _v1.10_

**control-manager** and **kube-scheduler** - They can be 1 version older than the kube-apiserver. eg - _v1.10_ or _v1.09_

**kubelet** and **kube-proxy** - They can be 2 versions older than kube-apiserver eg - _v1.10_ or _v1.9_ or _v1.8_

**kubectl** - It can be 1 verion later than kube-apiserver, same as kube-apiserver or 1 version older. eg - _v1.11_ or _v1.10_ or _v1.9_


## 3 Strategies for version upgrades -

In each case, first take down master node and upgrade the software, then deploy it back. The worker nodes will still keep serving the app. But new deployments won't be possible.

1. Take down all the worker nodes, then make the upgrades and deploy back up. This will cause the downtime.

2. Take down one worker node at a time with `drain` strategy where the pods move to other worker nodes.

3. Deploy a new node with the new software version, then decommission all the old ones.
