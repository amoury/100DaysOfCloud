# Kubernetes Networking - Ingress

## Introduction
This section deals with Kubernetes Networking.

## Notes about the Kubernetes Certificates

3 types of certificates in Kubernetes

1. Server Certificates - Own set of public and private keys that belong to the server
2. Client Certificates - Owned by the client
3. Root Certificates - Owned by the Certificate Authority (CA)


### Various Certificates in K8S

**Server Certificates**

1. Kube-API Server - `apiserver.crt` and `apiserver.key`
2. ETCD Server - `etcdserver.crt` and `etcdserver.key`
3. Kubelet Server - `kubelet.crt` and `kubelet.key`


**Client Certificates**

1. Admin - Needs his own certificate to communicate with kube-api server (`admin.crt` & `admin.key`)
2. Kube-Scheduler - (`scheduler.crt` & `scheduler.key`)
3. Kube-Controller-Manager => `controller-manager.crt` and `controller-manager.key`
4. Kube-Proxy => `kube-proxy.crt` and `kube-proxy.key`


### Generate the certificates

