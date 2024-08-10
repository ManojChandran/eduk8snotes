# Introduction 
Last chapter we learned about the Kubernetes probes, how probes reflect the status and help in high availability. This will help us in having high available application in Kubernetes. Let's learn about these applications running in Kubernetes.

### What are application running in Kubernetes called?
Application running in Kubernetes are called workloads. Our workload is a single component or several that work together.

### Where does this workload run?
Our workloads run on set of PODs, POD represents a set of running container's on our cluster.

### What is the biggest challenge in managing individual pods?
When POD fails we need to get it back for the workload. Managing individual PODS is challenging and kubernets solves this by workload objects.
 
### What is a workload objects?
A workload object that represents a higher abstraction level than a Pod, and then the Kubernetes control plane automatically manages Pod objects on our behalf, based on the specification for the workload object we defined.
Kubernetes provide built in API to create workload object.

### What are the different workload objects available in Kubernetes?
* Deployments
* StatefulSet
* DaemonSet
* Job
* CornJob

### What does this workload objects help with?
These workload objects are build in API's to manage workloads.

### How can we extend this workload management capabilities? 
Using a custom resource definition, we can add in a third-party workload resource if we want a specific behavior that's not part of Kubernetes' core.

## Conclusion
We learned about workload and workload management API's, we will ellaborate on each of these workload management API's.