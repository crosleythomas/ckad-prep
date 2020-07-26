# Inspect and Monitor

## View Existing Resource(s)

To see what resources of a particular type are currently deployed use
```
kubectl get <resource_type>
```

To see what configuration the resource is deployed with, use the `describe` command.
```
# Describe all resources of a certain type
kubectl describe <resource_type>

# Describe a specific resource
kubectl describe <resource_type> <name>
```



## View logs for a Resource
```
# To view a pod's logs
kubectl logs <pod_name>

# To tail the logs
kubectl logs -f <pod_name>
```

## Exec into a Container

Sometimes it can help to [get a shell into a running container](https://kubernetes.io/docs/tasks/debug-application-cluster/get-shell-running-container/).

I find remember this particular command and all its variants hard to remember, but
fortunately just running `kubectl exec --help` will output lots of good examples.

The command you will probably want to get a shell in a pod is:
```
# Single container pod
kubectl exec <pod_name> -i -t -- bash -il

# Multi-container pod
kubectl exec <pod_name> -c <container_name> -i -t -- bash -il
```