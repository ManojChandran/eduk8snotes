# Introduction 
Last chapter we learned about Kubernetes architecture and learned about PODS, now lets learn about how PODS get scheduled in the nodes.

### Who schedules the PODS in kubernetes nodes?
Kube-scheduler selects an optimal node to run newly created or not yet scheduled (unscheduled) pods. It is the default scheduler for Kubernetes and runs as part of the control plane.

### What is the node called, when it meets the scheduling requirements?
Nodes that meet the scheduling requirements for a Pod are called `feasible nodes`.

### How Node selection happens?
kube-scheduler selects a node for the pod in a 2-step operation:

Filtering - scheduler filters all the nodes that can run POD.
Scoring - arrive at a score from 1 to 10, resource and other requirements defined by us.

Scheduler binds the POD in a node with highest score.

### Can we customize or instruct kube-scheduler on node assignment?
Yes, we can instruct kube-scheduler on how or on what scenarios a node can become feasible node.

### What are the supported ways of configure the filtering and scoring behavior?
There are two supported ways to configure the filtering and scoring behavior of the scheduler:

1. `Scheduling Policies` allow us to configure Predicates for filtering and Priorities for scoring.
2. `Scheduling Profiles` allow us to configure Plugins that implement different scheduling stages, including: QueueSort, Filter, Score, Bind, Reserve, Permit, and others.

### What are the scheduling plugins enabled by default?
* nodeName: Deploy our POD to a particular node match the name.
* nodeSelector: Deploy our POD to a particular set of nodes with same label names.
* Affinity: Deploy our POD matching our complex condition. It has two types `Node affinity` and `POD affinity`.
