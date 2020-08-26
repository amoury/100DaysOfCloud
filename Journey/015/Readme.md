# Kubernetes Security - Certificates

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

Step 1: Create a private key using `openssl` command - `openssl genrsa -out ca.key 2048`

Step 2: Generate Signing request - `openssl req -new -key ca.key "/CN=KUBERNETES-CA" -out ca.csr`. The Certificate Signing Request(CSR) is like your certificate but without the signature. (CN - Common Name)

Step 3: Sign the certificate using `openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt`. Since this certificate is for CA (Certificate Authority) itself, it is self signed.

If you are generating certificate for some other entity, you have to add the Certificate signing authority -

`openssl x509 -req -in admin.csr -CA ca.crt -CAkey ca.key -out admin.crt`







