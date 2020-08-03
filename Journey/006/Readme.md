![placeholder image](https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1200&q=80)

# Kubernetes Cluster Maintenance

## Introduction
Knowing how to properly backup your running pods and take down nodes for upgrades is important for an administrator.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes on How to Backup and Restore the Cluster

What can you backup?

1. **Resource Configuration** - Backup of Resource definition files. `kubectl get all --all-namespaces -o yaml > all-resources.yaml`
2. **ETCD** - Data Dir where ETCD DB is stored can be backed up. 
You can use `etcdctl snapshot save snapshot.db`

To restore from ETCD,
- First stop `kube-apiserver` with the command  - `service kube-apiserver stop` and then run the command `etcdctl restore snapshot.db` 


