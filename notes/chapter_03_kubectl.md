# Introduction 
Lets learn to communicate with kubernetes with `kubectl` command.

### What is kubectl?
The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters.

### How to check the kubectl version installed?
Display the Kubernetes version running on the client and server.
```sh
kubectl version
```

### What are the basic cluster managemant commands?
Display endpoint information about the master and services in the cluster.
```sh
kubectl cluster-info
```
Get the configuration of the cluster.
```sh
kubectl config view
```
Get a list of users.
```sh
kubectl config view -o jsonpath='{.users[*].name}'
```
List the API resources that are available.
```sh
kubectl api-resources
```
List the API versions that are available.
```sh
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
```sh
kubectl config set-cluster my-cluster --server=https://<API_SERVER_ADDRESS> --certificate-authority=<PATH_TO_CA_CERT>
```
Set the user credentials
```sh
kubectl config set-credentials my-user --client-certificate=<PATH_TO_CLIENT_CERT> --client-key=<PATH_TO_CLIENT_KEY>
```
Set the context
```sh
kubectl config set-context my-context --cluster=my-cluster --user=my-user
```

### How do you view, list and set context?
View the current context
```sh
kubectl config current-context
```
List all the context
```sh
kubectl config get-contexts
```
Switch to different context
```sh
kubectl config use-context <context-name>
```
Set specific context as current context
```sh
kubectl config set-context <context-name>
```
Modify a context to set a default namespace
```sh
kubectl config set-context <context-name> --namespace=<namespace>
```
Delete a context
```sh
kubectl config delete <context-name>
```

### How to find the kubeconfig file location?
We can use the following kubectl command to verfy the config file path.
```sh
kubectl config view -o jsonpath='{.paths[*]}'
``` 

### List down some general commands related to namespaces?
Create a namespace.
```sh
kubectl create namespace <namespace_name>
```
List one or more namespaces.
```sh
kubectl get namespace <namespace_name> 
```
Display the detailed state of one or more namespaces.
```sh
kubectl describe namespace <namespace_name>
```
Delete a namespace.
```sh
kubectl delete namespace <namespace_name>
```
Edit and update the definition of a namespace.
```sh
kubectl edit namespace <namespace_name>
```

### List down some general commands related to nodes?
List one or more nodes.
```sh
kubectl get node
```
Add or update the labels of one or more nodes.
```sh
kubectl label node
```
Display Resource usage (CPU/Memory/Storage) for nodes.
```sh
kubectl top node <node_name>
```
Drain a node in preparation for maintenance.
```sh
kubectl drain node <node_name>
```
Mark a node as unschedulable.
```sh
kubectl cordon node <node_name>
```
Mark node as schedulable.
```sh
kubectl uncordon node <node_name>
```
Delete a node or multiple nodes.
```sh
kubectl delete node <node_name>
```
Pods running on a node.
```sh
kubectl get pods -o wide | grep <node_name>
```

### List down commands to check events?
List recent events for all resources in the system.
```sh
kubectl get events
```
List Warnings only.
```sh
kubectl get events --field-selector type=Warning
```
List events sorted by timestamp.
```sh
kubectl get events --sort-by=.metadata.creationTimestamp
```
List events but exclude Pod events.
```sh
kubectl get events --field-selector involvedObject.kind!=Pod 
```
Pull events for a single node with a specific name.
```sh
kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name> 
```
Filter out normal events from a list of events.
```sh
kubectl get events --field-selector type!=Normal 
```

### List down commands to view logs?
Print the logs for a pod.
```sh
kubectl logs <pod_name>
```
Print the logs for the last 6 hours for a pod.
```sh
kubectl logs --since=6h <pod_name>
```
Get the most recent 50 lines of logs.
```sh
kubectl logs --tail=50 <pod_name>
```
Get logs from a service and optionally select which container.
```sh
kubectl logs -f <service_name> [-c <$container>]
```
Print the logs for a pod and follow new logs.
```sh
kubectl logs -f <pod_name>
```
Print the logs for a container in a pod.
```sh
kubectl logs -c <container_name> <pod_name>
```
Output the logs for a pod into a file named ‘pod.log’.
```sh
kubectl logs <pod_name> pod.log
```
View the logs for a previously failed pod.
```sh
kubectl logs --previous <pod_name>
```

## Conclusion
We learned the basic commands and understood how to connect kubernetes clusters.