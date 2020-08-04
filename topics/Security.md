# Security

The 4C's of Cloud Native Security
 * Cloud
 * Cluster
 * Container
 * Cdoe
 
Each layer of the Cloud Native security model builds upon the next outermost layer.
The Code layer benefits from strong base (Cloud, Cluster, Container) security layers.
You cannot safeguard against poor security standards in the base layers by addressing security at the Code level.

## RBAC (Role-Based Access Control)
Use RBAC (Role-Based Access Control) to protect the Kubernetes cluster components (i.e. who can create/delete a `ConfigMap` but not a `Secret`, etc.)


## SCC (Security Context Constraints)
Use SCC (Security Context Constraints) to protect the nodes that Pods are running on

**Motivation**
* "The container platform is protected with good RBAC practices from it's created object,
s but the node may not be. That is where a Pod may not be able to delete an object in 
etcd using the API because it's restricted by RBAC, but it may delete important files in 
the system and even stop kubelet if properly programmed for that."
* "Enable a distinct isolation between a container and the host/node it runs on"

**tl;dr**: Use the `SecurityContext` field in a `Pod` or `Container` spec to specify what
processes running can and can't do

###`PodSecurityContext`
Setting the `securityContext` field in the Pod specification
will make the settings apply to all Containers in the Pod.

Example:
```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  volumes:
  - name: sec-ctx-vol
    emptyDir: {}
  containers:
  - name: sec-ctx-demo
    image: busybox
    command: [ "sh", "-c", "sleep 1h" ]
    volumeMounts:
    - name: sec-ctx-vol
      mountPath: /data/demo
    securityContext:
      allowPrivilegeEscalation: false
```

###`SecurityContext`
"Security settings that you specify for a Container apply only to the individual Container,
and they override settings made at the Pod level when there is overlap. 
Container settings do not affect the Pod's Volumes."

Example:
```
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo-2
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: sec-ctx-demo-2
    image: gcr.io/google-samples/node-hello:1.0
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
```

## Resources
* [Overview of Cloud Native Security](https://kubernetes.io/docs/concepts/security/overview/)
* [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/)
* [What is SELinux?](https://www.redhat.com/en/topics/linux/what-is-selinux)
* [Introduction to Security Contexts and SCCs](https://www.openshift.com/blog/introduction-to-security-contexts-and-sccs)
* [Configure a Security Context for a Pod or Container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)
* [Defining Privileges and Access Control Settings for Pods and Containers in Kubernetes](https://medium.com/kubernetes-tutorials/defining-privileges-and-access-control-settings-for-pods-and-containers-in-kubernetes-2cef08fc62b7)
* [Discretionary access control](https://en.wikipedia.org/wiki/Discretionary_access_control)
