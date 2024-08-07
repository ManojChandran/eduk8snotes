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

###         

### How can we identify the Objects?
We can give `name`  that is unique for that type of resource. ( eg name: nginx-demo )

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
We use labels and selectors to group name them and refer them as group. Labels - they are key/value pairs that are attached to objects such as Pods.

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
> If you don't undertsnd the yaml, Don't panic. We will deal with it in detail.


### How to communicate with the kubernetes control plane?
Kubernetes provides a command line tool named 'kubectl' for communicating with a Kubernetes cluster's control plane, using the Kubernetes API.

### What is kubectl?
The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters.
