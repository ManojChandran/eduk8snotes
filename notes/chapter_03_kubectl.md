# Introduction 
Lets learn to communicate with kubernetes with `kubectl` command.

### What is kubectl?
The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters.

### How to check the kubectl version installed?
Display the Kubernetes version running on the client and server.
```
kubectl version
```

### What are the basic cluster managemant commands?
Display endpoint information about the master and services in the cluster.
```
kubectl cluster-info
```
Get the configuration of the cluster.
```
kubectl config view
```
Get a list of users.
```
kubectl config view -o jsonpath='{.users[*].name}'
```
List the API resources that are available.
```
kubectl api-resources
```
List the API versions that are available.
```
kubectl api-versions
```

### How to format the command output?
kubectl provides formatting flag.
> -o=json : Output a JSON formatted API object </br>
> -o=yaml	: Output a YAML formatted API object </br>
> -o=wide	: Output in the plain-text format with any additional information, and for pods, the node name is included </br>

### How do you connect to an external Kubernetes cluster?
First we need to fins out the necessary information such as API server URL, authentication credentials, and context settings. `kubeconfig` file contains this information and we need to get it forom the Kubernetes cluster admin. Then we set the context to use the external kubernetes cluster. 

### What is kubeconfig?
`kubeconfig` is a configuration file used by kubectl and other Kubernetes tools to interact with a Kubernetes cluster. It contains the context by which we interact with the external cluster.
* Location of the cluster you want to connect to
* What user you want to authenticate as
* Data needed in order to authenticate, such as tokens or client certificates

### What is context in Kubernetes?
A context is a combination of fours main elements:
`Cluster`: The specific Kubernetes cluster you want to connect to. </br>
`User`: The user account with credentials to authenticate to the Kubernetes cluster.</br>
`Namespace`: The default namespace that kubectl commands will operate in if no namespace is specified in the command.</br>
`Authentication`: Methods and certicate details.</br>

### How to create a kubeconfig?
Set the cluster information
```
kubectl config set-cluster my-cluster --server=https://<API_SERVER_ADDRESS> --certificate-authority=<PATH_TO_CA_CERT>
```
Set the user credentials
```
kubectl config set-credentials my-user --client-certificate=<PATH_TO_CLIENT_CERT> --client-key=<PATH_TO_CLIENT_KEY>
```
Set the context
```
kubectl config set-context my-context --cluster=my-cluster --user=my-user
```

### How do you view, list and set context?
View the current context
```
kubectl config current-context
```
List all the context
```
kubectl config get-contexts
```
Switch to different context
```
kubectl config use-context <context-name>
```
Set specific context as current context
```
kubectl config set-context <context-name>
```
Modify a context to set a default namespace
```
kubectl config set-context <context-name> --namespace=<namespace>
```
Delete a context
```
kubectl config delete <context-name>
```

### How to find the kubeconfig file location?
We can use the following kubectl command to verfy the config file path.
```
kubectl config view -o jsonpath='{.paths[*]}'
``` 

### List down some general commands related to namespaces?
Create a namespace.
```
kubectl create namespace <namespace_name>
```
List one or more namespaces.
```
kubectl get namespace <namespace_name> 
```
Display the detailed state of one or more namespaces.
```
kubectl describe namespace <namespace_name>
```
Delete a namespace.
```
kubectl delete namespace <namespace_name>
```
Edit and update the definition of a namespace.
```
kubectl edit namespace <namespace_name>
```

### List down some general commands related to nodes?
List one or more nodes.
```
kubectl get node
```
Add or update the labels of one or more nodes.
```
kubectl label node
```
Display Resource usage (CPU/Memory/Storage) for nodes.
```
kubectl top node <node_name>
```
Drain a node in preparation for maintenance.
```
kubectl drain node <node_name>
```
Mark a node as unschedulable.
```
kubectl cordon node <node_name>
```
Mark node as schedulable.
```
kubectl uncordon node <node_name>
```
Delete a node or multiple nodes.
```
kubectl delete node <node_name>
```
Pods running on a node.
```
kubectl get pods -o wide | grep <node_name>
```

### List down commands to check events?
List recent events for all resources in the system.
```
kubectl get events
```
List Warnings only.
```
kubectl get events --field-selector type=Warning
```
List events sorted by timestamp.
```
kubectl get events --sort-by=.metadata.creationTimestamp
```
List events but exclude Pod events.
```
kubectl get events --field-selector involvedObject.kind!=Pod 
```
Pull events for a single node with a specific name.
```
kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name> 
```
Filter out normal events from a list of events.
```
kubectl get events --field-selector type!=Normal 
```

### List down commands to view logs?
Print the logs for a pod.
```
kubectl logs <pod_name>
```
Print the logs for the last 6 hours for a pod.
```
kubectl logs --since=6h <pod_name>
```
Get the most recent 50 lines of logs.
```
kubectl logs --tail=50 <pod_name>
```
Get logs from a service and optionally select which container.
```
kubectl logs -f <service_name> [-c <$container>]
```
Print the logs for a pod and follow new logs.
```
kubectl logs -f <pod_name>
```
Print the logs for a container in a pod.
```
kubectl logs -c <container_name> <pod_name>
```
Output the logs for a pod into a file named ‘pod.log’.
```
kubectl logs <pod_name> pod.log
```
View the logs for a previously failed pod.
```
kubectl logs --previous <pod_name>
```

## Conclusion
We learned the basic commands and understood how to connect kubernetes clusters.