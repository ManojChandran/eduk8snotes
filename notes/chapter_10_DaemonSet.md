# Introduction 
Last chapter we discussed about the workload and workload managements objects, we will learn in detail on `daemonSet` workload management objects.

### What is a DaemonSet?
DaemonSet is a kind of deployment, where it mandate Nodes to run a particular POD. It is particularly useful for deploying cluster-level services and background processes that needs to be available on each node.

### What are the typical use case of DaemonSet?
* Running a log collection daemon on every node
* Running a node monitoring daemon on every node
* Running a cluster storage daemon on every node



## Conclusion
We covered the