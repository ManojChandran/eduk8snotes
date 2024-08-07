# Introduction 
Let's discuss about workloads, application running in kubernets. 

### What is the biggest challenge in managing individual pods?
Our workloads run on a container in POD and when POD fails we need to get it back for the workload. Managing individual PODS like this will be challenging, kubernets solves this by `workload objects`.

### What is a `workload objects`?
A `workload object` that represents a higher abstraction level than a Pod, and then the Kubernetes control plane automatically manages Pod objects on our behalf, based on the specification for the `workload object` we defined.
> Kubernetes provide built in API to create `workload object`.

### What are the different `workload objects` available in Kubernetes?
* Deployments
* StatefulSet
* DaemonSet
* Job
* CornJob

## Conclusion