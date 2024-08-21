# Introduction 
Last chapter we discussed about the workload and workload managements objects, we will learn in deatil each of the workload management objects.

### What is a deployment?
A Kubernete `deployment` provides declarative updates for Pods and ReplicaSets.

### Why Deployments when we have PODS?
A `pod` is the smallest logical unit that we can deploy into a kubernetes cluster. But pod deployment will restrict us from harnessing power of kubernetes, `deployment` will help in below featues
* Declarative Updates and Rollbacks
* Self-Healing
* Scaling
* Multi-Version Support
* Resource Management
* Cross-Cluster Deployments

### How deployment works?
We describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate.

### How do Deployments ensure application availability?
Deployment Controller changes the actual state to the desired state at a controlled rate, making sure application highly available.

### What are rolling updates in Kubernetes?
A rolling update allows a Deployment update to take place with zero downtime. It does this by incrementally replacing the current Pods with new ones.

### What is a deployment strategy?
A deployment strategy is a way to change or upgrade an Kubernetes workloads (Application) with less downtime ever possible.

### What are the different deployment strategies?
* Rolling deployment
* Recreate deployment
* Ramped slow rollout
* Best-effort controlled rollout
* Blue/green deployment
* Canary deployment
* Shadow deployment
* A/B testing

### How does Kubernetes handle application rollbacks?
Kubernetes handles application rollbacks by scaling down the replica set for the updated version and scaling up the replica set for the previous version. This redirects traffic back to the previous version of the application.

## Conclusion
We covered the