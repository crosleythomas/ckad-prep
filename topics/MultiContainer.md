# Multi-Container Pods
* Ambassador
* Adaptor
* Sidecar

## Sidecar Pattern
The sidecar pattern consists of a main application—i.e. your web application—plus a helper container with a responsibility that is essential to your application, but is not necessarily part of the application itself.

The most common sidecar containers are logging utilities, sync services, watchers, and monitoring agents. It wouldn't make sense for a logging container to run while the application itself isn't running, so we create a pod that has the main application and the sidecar container. Another benefit of moving the logging work is that if the logging code is faulty, the fault will be isolated to that container—an exception thrown in the nonessential logging code won't bring down the main application.

Click here for an example pod using the sidecar pattern for log management

## Adapter Pattern
The adapter pattern is used to standardize and normalize application output or monitoring data for aggregation.

As a simple example, we have a cluster-level monitoring agent that tracks response times. Say we have a Ruby application in our cluster that writes request timing in the format [DATE] - [HOST] - [DURATION], while another Node.js application writes the same information in [HOST] - [START_DATE] - [END_DATE].

The monitoring agent can only accept output in the format [RUBY|NODE] - [HOST] - [DATE] - [DURATION]. We could force the applications to write output in the format we need, but that burdens the application developer, and there might be other things depending on this format. The better alternative is to provide adapter containers that adjust the output into the desired format. Then the application developer can simply update the pod definition to add the adapter container and they get this monitoring for free.

## Ambassador Pattern
The ambassador pattern is a useful way to connect containers with the outside world. An ambassador container is essentially a proxy that allows other containers to connect to a port on localhost while the ambassador container can proxy these connections to different environments depending on the cluster's needs.

One of the best use-cases for the ambassador pattern is for providing access to a database. When developing locally, you probably want to use your local database, while your test and production deployments want different databases again.

Managing which database you connect to could be done through environment variables, but will mean your application changes connection URLs depending on the environment. A better solution is for the application to always connect to localhost, and let the responsibility of mapping this connecting to the right database fall to an ambassador container. Alternatively, the ambassador could be sending requests to different shards of the database—the application itself doesn't need to worry.

## Resources
* [Multi-Container Pod Design Patterns in Kubernetes](https://matthewpalmer.net/kubernetes-app-developer/articles/multi-container-pod-design-patterns.html)

