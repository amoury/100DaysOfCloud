![placeholder image](https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1200&q=80)

# Kubernetes Security

## Introduction
Knowing how to properly backup your running pods and take down nodes for upgrades is important for an administrator.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Security

When it comes to security - we need to answer 2 questions - 

1. Who can access the cluster (Authentication)
2. What can they do? (Authorization)

Since `kube-apiserver` is the most important component of the cluster and can control everything on the cluster, this is the first component to secure.

### Authentication

Various approaches - 

1. Files - Username and passwords
2. Files - Username and tokens
3. Certificates
4. External Authentication providers - LDAP
5. Service accounts for the machines


### Authorization 

1. RBAC Authorization (Role Based Access Control)
2. ABAC Authorization
3. Node Authorization
4. Webhook Mode


### TLS Certificates

All the components such as ETCD Cluster, Controller Manager, Scheduler, Kube-proxy and Kubelet are all secured using TLS Encryption

### Network Policies
To restrict communication access between the pods.
