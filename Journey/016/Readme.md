# Kubernetes Security - Certificates API

## Introduction
This section deals with Kubernetes Certificates API.

## Notes about the Kubernetes Certificates

**Manual Way to create and assign certificates for new user** - 

When a user wants to connect to the cluster, they need a certificate approved from the CA server. So the new user first creates her own private key, generates the Certificate Signing Request (CSR) and sends it to the admin. The admin then takes the signing request to the CA server, gets it signed by the CA server using his Root certificate and private key, thereby generating a certificate and then sends it back to the new user.


CA server - 

CA is basically a key and a pair of certificate file we generated. Anyone having access to these files can sign the certificates for other components. So these files need to be protected and hence we keep them in a fully secured server. That server becomes the CA server.

Currently we store thse files on the master node, so master node also becomes the CA server.

