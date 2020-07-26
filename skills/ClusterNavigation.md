# Navigating Between Clusters

The CKA and CKAD exams are completed on multiple clusters, read [here](https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad#cka-and-ckad-environment).

Note:
* At the start of each task you'll be provided with the command to ensure you are on the correct cluster to complete the task.
* Where no explicit namespace is specified, the default namespace should be acted upon.

## [Configuring Access to Multiple Clusters](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)

First, the basics of how access to multiple clusters is set up.

Access to Kubernetes clusters (and users, and contexts) is set up via one or more config file(s) referred to as a `kubeconfig` file.  By default the file is located at `~/.kube/config`.

The `kubeconfig` file will be created for you so you only need to have a basic understanding of what it contains.

The `kubeconfig` file defines
* Clusters
* Users
* Contexts - a triple of (cluster, user, namespace)

Contexts are most relevant to you because you will be switching **contexts** for different problems. 

The important skill to know for the CKAD is how to switch between the pre-defined contexts.


## Switching Between Clusters

Get your current context `kubectl config current-context`

Switch to a different context `kubcetl config use-context <context-name>`

Yep, that's pretty much it.


## Troubleshooting

Examine the `kubeconfig` file
* `echo $KUBECONFIG`
* Check the contents of that file
