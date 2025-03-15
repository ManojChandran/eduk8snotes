# Introduction
Kubernetes is growing and more people are adopting it, lets discuss on collaboration in kuberentes.

### What is Helm?
Helm is a `package manager` for kubernetes, which helps to simplify deployment, management and upgrading of application. It is a tool that allow us to package and deploy applications and services on a kubernetes cluster.

### How Helm does its packaging?
Helm uses a packaging format called charts.

### What is a chart?
A `chart` is a collection of files that describes a set of related kubernetes resources.

### What is a repository?
A `repository` is the place where charts are collected and stored.

### What is a release?
A `release` is an instance of a chart running in a kubernetes cluster. It contains Kubernetes objects, such as ConfigMaps, Secrets, Deployments and Pods.

### Why we use Helm?
Helm charts provides a higher level of abstraction, minimizing the learning curve and allow a new person to Kubernetes to get started quickly. It shines in their customizability, leveraging templates, variables and value files to facilitate the management of intricate deployments.
* It makes application deployement easy
* It standardize deployemnt and make it reuseable
* Improves developer productivity
* It reduces deployment complexity

### How does Helm communicate with kubernetes?
Helm client and library are written in go programming language, the library uses the kubernetes client library to communicate with kubernetes.

### Where can we find the helm package?
We can find the Helm packages in [ArtifactHub](https://artifacthub.io/)

### What is the difference between Helm charts and Helm repo?
A chart is a Helm package and A repo is the place where charts can be colected and shared.

### What is the difference between Helm v2 and v3?

### Give basic helm commands?
Here are some basic `helm` commands;
#### helm installation & setup
```unix
helm version                     # Check helm version
```
#### Working with charts
```
helm search repo <chart-name>
helm pull <repo/chart-name>
helm show values <repo/chart-name>
```
#### Installing & Managing releases
```
helm install <release-name> <repo/chart-name>
helm list
helm upgrade <release-name> <chart>
helm rollback <release-name> <rev>
hel uninstall <release-name>
```
#### Inspecting & Debugging 
```
helm status <release-name>
helm history <release-name>
helm get all <release-name>
helm install <relase-name> --debug <chart>
helm install <relase-name> --dry-run <chart>
helm template <chart>
helm lint <chart>
```

#### Customizing Deployemnts
```
helm install <relase-name> <chart> --set key=value
helm install <relase-name> <chart> -f myvalues.yaml
```

#### Repository management
```
helm repo add sonarqube https://SonarSource.github.io/helm-chart-sonarqube
helm repo update
helm repo list
helm repo remove <repo-name>
```

