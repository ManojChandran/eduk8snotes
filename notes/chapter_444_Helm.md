# Introduction
After learning kubernetes basic, let discuss on collaboration in kuberentes.

### What is Helm?
Helm is a tool that allows us to package and deploy applications and services on kubernetes clusters. It is a package manager for kubernetes.

### How Helm does its packaging?
Helm uses a packaging format called charts.

### What is a chart?
A chart is a collection of files that describe a related set of kubernetes resources.

### Why we use Helm instead of Kubernetes?
Helm charts provides a higher level of abstraction, minimizing the learning curve and allow newcommers to Kubernetes to get started quickly. It shines in their customizability, leveraging templates, variables and value files to facilitate the management of intricate deployments.

### How does Helm communicate with kubernetes?
Helm client and library are written in go programming language, the library uses the kubernetes client library to communicate with kubernetes.

### Where can we find the helm package?
We can find the Helm packages in [ArtifactHub](https://artifacthub.io/)

### What is the difference between Helm charts and Helm repo?
A chart is a Helm package and A repo is the place where charts can be colected and shared.

### What is the difference between Helm v2 and v3?







