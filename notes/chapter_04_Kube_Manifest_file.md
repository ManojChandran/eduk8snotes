# Introduction 
Last chapter we learned about Kubernetes architecture, now lets learn about how we create.

### What is a manifest file?
A Kubernetes manifest file is a YAML or JSON file used to define the desired state of objects within a Kubernetes cluster. It contains `record of intent`.

### What are the key components of a manifest file?
* apiVersion: Specifies the version of the Kubernetes API to use for creating the object.
* kind: Specifies the type of Kubernetes resource being created (e.g., Pod, Service, Deployment).
* metadata: Provides metadata about the object, including its name, namespace, labels, and annotations.
* spec: Defines the desired state of the object, including the configuration details specific to the resource type.

### How can you fetch details about resource apiVersion, group..etc?
List the API resources that are available.
```
kubectl api-resources
```

### Write a sample manifest yaml?
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```
### How to implement this manifest file?
```
kubectl apply -f nginx_demo.yml
```
### How can test manifest file before applying?
```
kubectl apply --dry-run=client -f nginx_demo.yml -o yaml
```

### What is metadata used for?
metadata: Provides metadata about the object, including its name, namespace, labels, and annotations.

### How labels in meta data help?
The `labels` in metadata help to define key value pair attached to kubernetes `objects`. They are used to organize, categorize, and select subsets of objects.

> It creates a reference point for other manifest files to refer this object. It work in combination `labels` and `selectors`.

Example for label
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
```
Example for Selector refering label
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: web
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80

```

### How to add a comment in the manifest file?
Use "#" to add comment in manifest file.
```yaml
# This deployment creates 3 replicas of the nginx container
```

## Conclusion
We learned how to create manifest file, apply them to create object and refer them using selectors.