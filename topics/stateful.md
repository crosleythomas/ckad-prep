
```
A volume will be in one of the following phases:

Available -- a free resource that is not yet bound to a claim
Bound -- the volume is bound to a claim
Released -- the claim has been deleted, but the resource is not yet reclaimed by the cluster
Failed -- the volume has failed its automatic reclamation
```

Volume
Persistent Volume
Persistent Volume Claim

What actually gets "mounted" onto the container?

"Two knobs which are particularly important to think about in any deployment are the **binding** and **retention modes**. We’ll cover these, below."

## Background Reading and Resources

Good intro and deep dive blog posts
* https://platform9.com/blog/stateful-applications-with-kubernetes/
* https://platform9.com/blog/kubernetes-storage-dynamic-volumes-and-the-container-storage-interface/
* https://platform9.com/blog/tutorial-dynamic-provisioning-of-persistent-storage-in-kubernetes-with-minikube/

Docs on the (CSI) Container Storage Interface
* https://kubernetes.io/blog/2019/01/15/container-storage-interface-ga/
* https://kubernetes-csi.github.io/docs/
* https://cloud.google.com/anthos/gke/docs/on-prem/how-to/install-csi-driver

Some good background reading on how plugins in general (of which CSI implementations are an example)
are implemented in Kubernetes
* https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/#device-plugin-registration

Binding
* https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode
* https://kubernetes.io/docs/concepts/storage/persistent-volumes/#binding

Reclaim Policy
* https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy
* https://kubernetes.io/docs/tasks/administer-cluster/change-pv-reclaim-policy/#why-change-reclaim-policy-of-a-persistentvolume


```
Current reclaim policies are:

Retain -- manual reclamation
Recycle -- basic scrub (rm -rf /thevolume/*)
Delete -- associated storage asset such as AWS EBS, GCE PD, Azure Disk, or OpenStack Cinder volume is deleted
```

Access Modes
* https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes
