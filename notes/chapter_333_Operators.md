# Introduction
Lets deep dive on the Operators in Kubernetes.

### What is a kubernetes Operator?
Operators are clients of the Kubernetes API that act as controllers for a Custom Resource.

### What do you mean by Resource in Kubernetes?
A Resource is an endpoint in the Kubernetes API that stores a collection of API objects of a certain kind.

### What are Custom Resource?
A Custom Resource is an object that extends the Kubernetes API or allows you to introduce your own API into a project or a cluster.

### How can we create the custom Object?
Custom resouce objects are created by creating an object from a Custom Resource Definition (CRD).

### What is CRD?
A CRD stands for Custom Resource Definition, its a file that let us define our own object kinds and lets the API Server handle the entire lifecycle.

____
### How can we write a operator?
### What functions should my operator perform?
### What API permissions will my operator need to perform those functions?
### What framework should I write my operator?

- All operators are controllers and all controllers are not operators
- A controller that does nothing stateful is just a controller
## References
[Operator hub](https://operatorhub.io/) </br>
[Write Kubernetes operator from Scratch](https://www.youtube.com/watch?v=LLVoyXjYlYM) </br>