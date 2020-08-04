![placeholder image](https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1200&q=80)

# Kubernetes Storage

## Introduction
Knowing how to properly backup your running pods and take down nodes for upgrades is important for an administrator.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Storage

- By nature docker containers are transient in nature. Containers are also supposed to be stateless. So all the data created by the container is typically destroyed when the container is killed, unless....

We attach a volume to the container. In this case, the data is persisted in the volume.

It's the same mechanism in K8s, pod is transient by nature and doesn't persist the data unless a volume is attached.

### PersistentVolume

- Cluster wide pool of central storage configured by admin to be used by users deploying application in the cluster. Users can use PV using PersistentVolumeClaims (PVC) 

Administrator create PersistentVolumes and the user creates a claim to claim a PersistentVolume.

Different types of _persistentVolumeReclaimPolicy_ :

1. **Retain** - It will remain until manually deleted. Not available for reuse by any other claims.
2. **Delete** - As soon as claim is deleted, the volume is deleted as well, thus freeing up the resources.
3. **Recycle** - Data is scrubbed before making the volume available to other claims.
