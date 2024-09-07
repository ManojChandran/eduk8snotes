# Introduction 
Last chapter we discussed about the `ReplicaSet`, an important concept in workload managements objects. This chapter we will learn in detail on the workload management object `Deployment`.

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
Deployment Controller changes the actual state to the desired state at a `controlled rate`, making sure application highly available.

### Give a sample deployment manifest?
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
### Give me the basic deployment commands?
```
kubectl create -f deployment-def.yml
```
```
kubectl get deployments
```
```
kubectl apply -f deployment-def.yml
```
```
kubectl rollout status deployment/myapp-deployment
```
```
kubectl rollout history deployment/myapp-deployment
```
```
kubectl rollout undo deployment/myapp-deployment
```
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

### What is the default deployment strategy?
A Rolling deployment is the default deployment strategy in kubernetes.

### What is a `Rolling` deployment?
The Rolling deployment is the default strategy that allow, one by one replacement of old version of the application with new version.

### How we can control the Rolling deployment?
Rolling deployment can be controlled by two optional prameters in manifest file, `maxSurge` and `maxUnavialable`.
* MaxSurge specifies the maximum number of pods the Deployment is allowed to create at one time.
* MaxUnavailable specifies the maximum number of pods that are allowed to be unavailable during the rollout.

```yaml
spec:
  replicas: 10
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 3
      maxUnavailable: 1
```

### What is a `Recreate` deployment?
Recreate deployment is a strategy that recreates and replaces old application with new one instantly. It has potential downtime.

### What is a `Blue-Green` deployment?
A blue-green deployment involves deploying an entire new application with new version side by side and re-routing traffic from old version to the new applicaton version, once the application is UP.

### What is a `Canary` deployment?
Canary deployment strategy uses deployments in subsets, new application versions are released to a small number of test users.

### How does Kubernetes handle application rollbacks?
Kubernetes handles application rollbacks by scaling down the replica set for the updated version and scaling up the replica set for the previous version. This redirects traffic back to the previous version of the application.

## Conclusion
We covered the kubernetes Deployment and Deployment strategies, as part of the work load management.