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


## Steps to carry out node upgrade

step 1: First run the command `kubeadm upgrade plan`. This will give you all the info about the latest available version. Typically the way to upgrade is - let's say you are on version 1.16 and the current stable version is 1.18, then the best way to upgrade is to first update to 1.17 and then to 1.18.

Step 2: If the kubeadm tool is not the latest, first upgrade the **kubeadm** tool

`kubeadm version` - to confirm the version.

Then type this command to upgrade the kubeadm version

```sh
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.18.x-00 && \
apt-mark hold kubeadm
```

Here is the link - https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/#upgrading-control-plane-nodes

Step 3 - Once this is complete, you need to first drain the node that you decided to upgrade. So if its master and any pods are scheduled on master, first drain the master node.

`kubectl drain master`

Step 4 - You can then run this command to perform the upgrade.

`kubeadm upgrade apply v1.18.0`

Step 5 - [Upgrade Kubelet and Kubectl](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/#upgrade-kubelet-and-kubectl)

```
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.18.x-00 kubectl=1.18.x-00 && \
apt-mark hold kubelet kubectl
```

Step 6 - Restart kubelet

```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

Step 7 - Make sure to uncordon the node 

`kubectl uncordon <cp-node-name>`


On worker nodes, we just need to upgrade kubelets

https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/#upgrade-worker-nodes
