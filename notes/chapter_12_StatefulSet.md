# Introduction 
Last chapter we discussed about the workload managements object `JOBS`. In this chapter,  we will learn in detail on  workload `StatefulSet` management object.

### What is a `stateful` application?
A `stateful application` is an application that needs to maintain and track its state between restarts, redeployments, or even across different instances of the application. This is sometimes know as sticky identity of the workload.

### What is a `StatefulSets`?
A `StatefulSet` is a Kubernetes controller designed to manage stateful applications.

### How `StatefulSets` support stateful appliation?
It manages stateful application by providing POD with unique, stable identity and hostname.

### When we use  `StatefulSets`?
We use `StatefulSets` for workloads, which require:
* Stable, unique netwrok identifier
* Stable, persistent storage
* Ordered, graceful deployment and scaling
* Ordered, Automated rolling updates

### Can you write a sample manifest file implementing `StatefulSets`?
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: "mysql"
  replicas: 3
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:5.7
          ports:
            - containerPort: 3306
          volumeMounts:
            - name: mysql-data
              mountPath: /var/lib/mysql
  volumeClaimTemplates:
    - metadata:
        name: mysql-data
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 10Gi
```
### What are the key components of `StatefulSets`?
* Service : Required for stable network identity.
* Pod Template : Defines the Pod specifications (container, image, ports, etc.).
* Persistent Storage : Ensures each Pod gets a dedicated PersistentVolume (PV).

### What is `persistent storage`?
Persistent storage in the context of computing and Kubernetes refers to a type of storage that retains data across application restarts, crashes, and shutdowns.

### What are types of `persistent storage`?
* Block Storage (e.g., AWS EBS, Google Persistent Disks): Raw storage volumes attached to instances, suitable for databases or applications requiring low-latency access.
* File Storage (e.g., NFS, Amazon EFS): Provides file-level access, allowing multiple instances to read and write from the same storage.
* Object Storage (e.g., Amazon S3, Google Cloud Storage): Ideal for storing unstructured data like logs, backups, or media files.

## Conclusion
We covered the