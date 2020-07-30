![placeholder image](https://images.unsplash.com/photo-1565264316550-a1811f0c4c75?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2016&q=80)

# Kubernetes Scheduling Approaches

## Introduction

Having a deeper understanding of the Kubernetes Architecture is important especially if you are aiming for a job as a DevOps Engineer or you are planning to appear for CKA exam i.e. Certified Kubernetes Administrator. 

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Architecture

Generally, **Kube-scheduler** is the component in K8s that is responsible for scheduling the pods on the nodes. But there are few different ways in which you can take control and manually schedule the pods on particular nodes -

1. Manual Scheduling - By giving node name to the pod definition file.
2. By assigning labels and selectors 
3. Adding taints and tolerations
4. Assigning node affinity
5. Using Daemonsets
6. Static Pods
