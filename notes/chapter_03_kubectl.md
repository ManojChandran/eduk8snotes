# Introduction 
Lets learn to communicate with kubernetes with `kubectl` command.

### What is kubectl?
The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters.

### What is kubeconfig?
`kubeconfig` is a configuration file used by kubectl and other Kubernetes tools to interact with a Kubernetes cluster. It contains information about clusters, users, namespaces, and authentication mechanisms, allowing you to manage multiple clusters and users from a single file.

### How to find the kubeconfig file location?
We can use the following kubectl command to verfy the config file path.
```
kubectl config view -o jsonpath='{.paths[*]}'
```
 
## Conclusion
We learned the basic commands and understood how to connect kubernetes clusters.