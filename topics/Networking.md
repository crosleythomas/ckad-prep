# Networking

## Network Policies

Alright, these aren't too bad. At least once you have the [Network Plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)
installed in your cluster. But hey, that's the cluster administrators' job!

Basically, all network traffic is allowed to/from pods by default in Kubernetes.
You use `NetworkPolicy` objects to restrict that traffic.

You will create a set of `ingress` and `egress` rules for one or more of:
* `podSelector`
* `namespaceSelector`
* `namespaceSelector and podSelector`
* `ipBlock`

And select pods, namespaces, or IP blocks to allow in/out.

## Resources
* [GKE Network Policy Demo](https://github.com/GoogleCloudPlatform/gke-network-policy-demo)
* [Network Policy Medium Challenge](https://medium.com/faun/kubernetes-ckad-weekly-challenge-6-networkpolicy-6cc1d390f289)