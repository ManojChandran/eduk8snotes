# Introduction
We are trying to learn kubernetes basics in this chapter, we learn by asking question and answering them.

### What is a kubernetes?
Kubernetes is an open source container orchestration engine for automating deployment, scaling, and management of containerized applications.

## How Kubernetes work?
Kubernetes ask us what state you we want and heart of the kubernetes is a fleet of controllers. Kubernetes controller is a control loop that watches the state of our cluster, then make changes to move the `current state` closer to the `desired state`.

<img src="../images/control_loop.png"  width="60%" height="30%"> 

### How Kubernetes understand what we want?
Kubernetes understand what we want by the `objects` we created.

### How controllers maintains the desired state?
Kubernetes realize our request as an `object` state and kubernetes continuously work on maintaining the request state. Each object has a object `spec` (describes desired state) and `status` (describes current state).

### How can we create object in Kubernetes?
A Kubernetes understand our requirement from Manifest file. Manifest file is a YAML or JSON file that describes the desired state of a Kubernetes object. We can request object creation in three ways 
* API                         
* kubectl 
* GUI

## Give an example for API request?
We write kubernetes API (record of intent), we express our request in .yaml format.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
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

### What will kubernetes do with our API request?
Kubernetes creates `objects`, Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster.

### What are the different Object Kinds, kubernetes understand?
1. Pods
2. Replica Sets
3. Services
4. Volumes
5. Namespaces
6. ConfigMaps and Secrets
7. Stateful Sets
8. Daemon Sets

### Why kubernetes are called k8's?
Entire kubernetes working depends on or modeled around 8 kubernetes kind offered. 

### How does kubernetes achive the orchestration?
An application state is requested as an object to kubernetes using API, Kubernetes recieves the request and maintain the state in a cluster. It is a Master and Worker node architecture, control plane act as a master and corresponding nodes act as workers with pods in it. <br />

<img src="../images/Kubernetes_cluster_architecture.png"  width="60%" height="30%">

### What are the major components of kubernetes?
Kubernetes components are classified as Control plane compoanents and Node components.

Control plane components consists of 
* kube-apiserver
* etcd
* kube-scheduler
* kube-controller-manager
* cloud-controller-manager

Node Components consist of 
* kubelet
* kube-proxy
* Container runtime

### What are Addons in kubernetes?
Add-ons extend the functionality of Kubernetes. Special listed Addons nare

* DNS
* Web UI (Dashboard)
* Container Resource Monitoring
* Cluster-level Logging
* Network Plugins

### Where are these objects stored?
Kubernetes stores the serialized state of objects by writing them into `etcd`.

### What is an etcd?
`etcd` is an open source distributed key-value store used to hold and manage the critical information that distributed systems need to keep running. 
* Replicated 
* Consistent
* Highly available
* Fast
* Secure

Kubernetes `etcd` stores state data, configuration data and meta data. `etcd` has a wait frunction which continiously monitor config and state, will notify kubernetes when there is a difference.

### How these Objects are identified?
Each object in your cluster has a Name that is unique for that type of resource. Every Kubernetes object also has a UID that is unique across your whole cluster. (eg name: nginx-demo )

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-demo
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

### How can we group these Objects and refer when needed?
We use labels and selectors to group name them and refer them as group.
Labels - they are key/value pairs that are attached to objects such as Pods.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: label-demo
  labels:
    environment: production
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

## Conclusion
We understood basic building block of kubernetes `objects` and learned about the components of kubernetes.