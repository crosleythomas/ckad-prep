# Create, Edit, and Destroy Resources

During the exam you will be asked to create and destroy resources.

Note:
* If you need to destroy/recreate a resource to perform a certain task, it is your responsibility to back up the resource definition appropriately prior to destroying the resource.


## Creating Resources

One of the key skills when creating resources on the CKAD is to do it quickly.  You don't want to write every single line
of YAML because that will eat up a lot of your exam time.  There are a few tricks to generate resource YAML files and
then edit only the portions you need. 

### Generating YAML

You use the create and run commands to generate YAML for a pods and other resources.
```
# For a Pod
kubectl run <name> —-image=<name>:<tag> -o yaml --dry-run > <name>.yaml

# For other resources
kubectl create <resource_type> <name> 
```

If you have an existing resource, you can export its definition.
```
kubectl get deployment <name> -o yaml --export > <name>.yaml
# Note: it seem the --export flag is deprecated but may still work
```

### Create Resources

If you just want to create resources on the fly, use
```
# For Pods
kubectl run <name> —-image=<name>:<tag>

# For other resources
kubectl create <resource_type> name
```

To create resources using YAML files there are two options:

```
# Imperatively
kubectl create -f <path_to_yaml>

# Declaratively
# Note: if there is an existing resource of the same type with the
# same name, kubernetes will do an in-place update of the existing resource.
kubectl apply -f <path_to_yaml>
kubectl apply -f <path_to_directory>/

```

## Editing Resources

**Option 1**
A simple way to directly edit fields in a text editor is to use the `kubectl edit` command 
with the resource you want to edit:
```
kubectl edit <resource_type> <name>
```

**Option 2**
If you have a YAML resource definition with the same type and name of an existing resource,
but with some fields changed, you can use `kubectl apply`.
```$xslt
kubectl apply -f <path_to_yaml>
```

**Option 3**
This option is different from 1 and 2 because it deletes the old resource
before re-creating the new resource. 
```
kubectl replace -f <path_to_yaml>
```
## Deleting Resources

There are several variants for deleting resources, all using the `kubectl delete` command.

Some examples:
```
# Delete a pod using the type and name specified in pod.json
kubectl delete -f ./pod.json

# Delete pods and services with same names "baz" and "foo"
kubectl delete pod,service baz foo

# Delete pods and services with label name=myLabel
kubectl delete pods,services -l name=myLabel

# Delete all pods and services in namespace my-ns
kubectl -n my-ns delete pod,svc --all
```