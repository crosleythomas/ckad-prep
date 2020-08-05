# Pod Design

## Labels, Selectors, and Annotations

* [**Label**](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/):
A key/value pair that is attached to objects, such as pods.
Used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system.
* [**Selector**](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors):
The core grouping primitive in Kubernetes.
Used to identify one or more Kubernetes Resources through their non-unique Label(s).
  * Can be used in YAML manifests, i.e. `nodeSelector.accelerator=nvidia-tesla-p100`
  * Can be used in `kubectl` commands, i.e. `kubectl get pods -l environment=production,tier=frontend`

You can also use selectors on more than just `Labels`, see [here](https://kubernetes.io/docs/concepts/overview/working-with-objects/field-selectors/).
* [**Annotation**](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/):
Annotations are similar to Labels in that they can attach meta-data to Kubernetes objects,
but are used for a different purposes (attaching **non-identifying** metadata) and can include
some characters in their value that Labels cannot include.

## Rolling Updates
* [Performing a Rolling Update](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/)
* [Interactive Tutorial](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-interactive/)

* When you use a Deployment, rolling updates are performed automatically 
* By default, the maximum number of Pods that can be unavailable during the update and the maximum number of new Pods that can be created, is one


## Rollbacks
