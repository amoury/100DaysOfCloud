![placeholder image](https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1200&q=80)

# Kubernetes Scheduling Approaches

## Introduction
Monioring the cluster and getting the container logs are important for an administrator.

## Prerequisite

I assume you have the knowledge of containers in general and Docker in particular.

## Notes about the Kubernetes Architecture

**Metrics Server** is the very basic and lightweight monitoring solution that we need to install. Then after sometime, typing the commands `k top nodes` or `k top pods` gives us analytics about the CPU and memory usage.

**Logging** - We can get the container logs using the command `k logs <pod-name> <container-name>`. Adding `-f` flag to the command enables us to watch the logs in real time.
