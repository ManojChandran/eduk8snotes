# Introduction 
In previous chapters, we learned about Kubernetes architecture and learned about PODS, now lets learn about how PODS get scheduled in the nodes.

### Who schedules the PODS in kubernetes nodes?
Kube-scheduler selects an optimal node to run newly created or not yet scheduled (unscheduled) pods. It is the default scheduler for Kubernetes and runs as part of the control plane.

### What is the node called, when it meets the scheduling requirements?
Nodes that meet the scheduling requirements for a Pod are called `feasible nodes`.

### How Node selection happens?
kube-scheduler selects a node for the pod in a 2-step operation:

* Filtering - scheduler filters all the nodes that can run POD. 
* Scoring - arrive at a score from 1 to 10, resource and other requirements defined by us.

Scheduler binds the POD in a node with highest score.

### Can we customize or instruct kube-scheduler on node assignment?
Yes, we can instruct kube-scheduler on how or on what scenarios a node can become feasible node.

### What are the supported ways of configure the filtering and scoring behavior?
There are two supported ways to configure the filtering and scoring behavior of the scheduler:

1. `Scheduling Policies` allow us to configure Predicates for filtering and Priorities for scoring.
2. `Scheduling Profiles` allow us to configure Plugins that implement different scheduling stages, including: QueueSort, Filter, Score, Bind, Reserve, Permit, and others.

### What are the scheduling plugins enabled by default?
nodeName: Deploy our POD to a particular node match the name.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
  nodeName: node1
```
nodeSelector: Deploy our POD to a particular set of nodes with same label names.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
  nodeSelector:
    disktype: ssd
    environment: production
```
Affinity: Deploy our POD matching our complex condition. It has two types `Node affinity` and `POD affinity`.
Node affinity : provides a more expressive and flexible way to specify rules for node selection
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: kubernetes.io/hostname
            operator: In
            values:
            - node1
```
POD affinity : allows you to specify that a Pod should be scheduled on a node where certain other Pods are running.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - frontend
        topologyKey: kubernetes.io/hostname
```

### What does `requiredDuringSchedulingIgnoredDuringExecution` tag means?
The `requiredDuringSchedulingIgnoredDuringExecution` ensures that the specified conditions are met at the time of scheduling. Once the Pod is scheduled, changes to the node conditions or labels do not affect the Pod's placement. This tag is useful for ensuring strict placement rules during the initial scheduling of Pods while allowing for flexibility afterward.

### What does `preferredDuringSchedulingIgnoredDuringExecution` tag means?
The `preferredDuringSchedulingIgnoredDuringExecution` provides guidelines for the scheduler to prefer certain nodes or conditions when placing Pods. These are soft constraints, meaning that if the preferred conditions cannot be met, the Pod will still be scheduled on another available node. This tag allows for more flexible scheduling, aiming to improve placement without being as restrictive as hard constraints.

* taints and tolerance :

## Conclusion
We learned about the POD scheduling process and methods availble.