# Introduction 
Last chapter we discussed about the workload and workload managements objects, we will learn in deatil each of the workload management objects. Before that we check on to an important concept of `ReplicaSet`.

### What is a ReplicaSet in Kubernetes?
ReplicaSet is a resource type responsible for maintaining a stable set of POD's. Purpose is to maintain high availability.

### How does a ReplicaSet ensure the desired number of Pods are running?
ReplicaSets in Kubernetes are designed to maintain the desired number of PODs. It continuously monitor the actual state of PODs against the desired state, take corrective actions of creating and deleting PODs.

### How do you scale a ReplicaSet?
* Using the kubectl scale Command
* Editing the ReplicaSet Manifest
* Using kubectl edit 
* Using Horizontal Pod Autoscaler (HPA)
* Scaling Through a Deployment

### How will replicaset decide on which Pod goes to which node? 
ReplicaSet doesn't directly decide which node a pod should be scheduled on. The actual decision of which node a pod goes to is handled by the Kubernetes Scheduler.
> By default, the Kubernetes Scheduler tries to balance the load by spreading pods across all available nodes. 

### How Labels and Selectors Work Together in a ReplicaSet?
Labels on Pods: When you define a ReplicaSet, you specify a pod template that includes labels. These labels are automatically applied to any pod created by the ReplicaSet.
Selectors in ReplicaSet: The selector in the ReplicaSet's spec matches these labels. The ReplicaSet then manages any pods that match this selector, ensuring that the specified number of replicas is always running.
  
### What happens to a ReplicaSet when its Pods are manually deleted?
When a pod that is managed by a ReplicaSet is manually deleted, the ReplicaSet will automatically respond by creating a new pod to replace the deleted one. This behavior ensures that the desired number of replicas specified in the ReplicaSet's configuration is always maintained.

### How can we set up a ReplicaSet to run in a specific namespace?
* We can specify the namespace in the metadata section of the ReplicaSet manifest file.
*Alternatively, use the --namespace flag with kubectl apply to deploy the ReplicaSet to a specific namespace.You can set a default namespace for your current kubectl context to avoid repeatedly specifying the namespace.

### What is the difference between ReplicaSet and ReplicationController?
ReplicaSets support set-based label selectors, whereas ReplicationControllers only support equality-based selectors.

> Kubernetes official recommendation: A Deployment that configures a ReplicaSet is now the recommended way to set up replication.

### How can we view the status of a ReplicaSet?
```
kubectl get replicaset [replicaset-name] -n [namespace]
```

## Conclusion
We covered the