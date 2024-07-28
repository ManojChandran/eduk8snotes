# Introduction 
Lets learn to communicate with kubernetes with `kubectl` command.

### What is kubectl?
The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters.

### How do you connect to an external Kubernetes cluster?
First we need to fins out the necessary information such as API server URL, authentication credentials, and context settings. `kubeconfig` file contains this information and we need to get it forom the Kubernetes cluster admin. Then we set the context to use the external kubernetes cluster. 

### What is kubeconfig?
`kubeconfig` is a configuration file used by kubectl and other Kubernetes tools to interact with a Kubernetes cluster. It contains the context by which we interact with the external cluster.

### What is context in Kubernetes?
A context is a combination of three main elements:
`Cluster`: The specific Kubernetes cluster you want to connect to.
`User`: The user account with credentials to authenticate to the Kubernetes cluster.
`Namespace`: The default namespace that kubectl commands will operate in if no namespace is specified in the command.

### How do you View, list and set context?
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
## Conclusion
We learned the basic commands and understood how to connect kubernetes clusters.