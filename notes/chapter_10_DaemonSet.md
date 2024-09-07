# Introduction 
Last chapter we discussed about the workload managements object `Deployment`. In this chapter,  we will learn in detail on `daemonSet` workload management object.

### What is a DaemonSet?
DaemonSet is a kind of deployment, where it mandate Nodes to run a particular POD. It is particularly useful for deploying cluster-level services and background processes that needs to be available on each node.

### What are the typical use case of DaemonSet?
* Running a log collection daemon on every node
* Running a node monitoring daemon on every node
* Running a cluster storage daemon on every node

### What is a Priviliged DaemonSet in kubernetes?
A Privileged DaemonSet is a type of DaemonSet where the pods it manages run in "privileged" mode. In Kubernetes, a privileged pod has elevated permissions on the host system, similar to the root user on a Linux machine. This elevated permission allows the pod to perform a wide range of system-level operations that are typically restricted.

## Conclusion
We covered the kubernetes DaemonSet, as part of the work load management.