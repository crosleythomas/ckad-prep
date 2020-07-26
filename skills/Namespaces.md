CKAD Notes:
* Where no explicit namespace is specified, the default namespace should be acted upon

## Overview

**[Namespaces Definition](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)**: Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces.

Kubernetes starts with four initial namespaces:
* **default** - The default namespace for objects with no other namespace
* **kube-system** - The namespace for objects created by the Kubernetes system
* **kube-public** - This namespace is created automatically and is readable by all users (including those not authenticated). This namespace is mostly reserved for cluster usage, in the case that some resources should be visible and readable publicly throughout the whole cluster. The public aspect of this namespace is only a convention, not a requirement.
* **kube-node-lease** - This namespace for the lease objects associated with each node which improves the performance of the node heartbeats as the cluster scales.

Namespaces are typically created to segment related kubernetes resources into logic groups.

## Working with Namespaces

```

# List namespaces
kubectl get namespace

# Creating a Namespace
kubectl create namespace <name>

# For every other kubectl you pretty much just need to add the argument
# --namespace=<namespace>
# to scope what you're trying to do to a particular namespace.
# 
# Examples:
kubectl run nginx --image=nginx --namespace=<insert-namespace-name-here>

kubectl get pods --namespace=<insert-namespace-name-here>

# If you are interacting with a single namespace repeatedly you can run
kubectl config set-context --current --namespace=<insert-namespace-name-here>

```