# Introduction 
Last chapter's we discussed about the workload managements objects. It will be intersting to know where is this application knowledge stored in kubernetes.

### What is the single source of truth in a Kubernetes cluster?
The single source of truth in a Kubernetes cluster is the `etcd` datastore.

### What is a ETCD?
`etcd` is a distributed, reliable key-value store that is used to store the critical state and configuration data of a Kubernetes cluster. It serves as the backbone of Kubernetes' control plane, acting as the single source of truth for all cluster data.

### Why etcd is Important in Kubernetes?
Cluster State Storage: 
* etcd holds the entire cluster's state, including node information, resource definitions, pod statuses, service configurations, and secrets.

High Availability: 
* etcd’s distributed nature ensures that even if part of the system fails, the cluster can continue functioning by accessing the replicated state data.

Control Plane Dependency: 
* Kubernetes control plane components like the API server, controller-manager, and scheduler depend on etcd to read and write the desired state of the cluster.

### When ETCD is unavailable, will the kubernetes cluster "go down"?
The Kubernetes cluster does not "go down" when etcd is unavailable, but its control plane becomes non-functional, meaning no new workloads can be managed or scheduled. The existing workloads continue to run, but the cluster becomes unable to perform essential management functions until etcd is restored.

### Where does etcd run in a Kubernetes cluster?
1. In a self-managed Kubernetes cluster, etcd typically `runs on the control plane nodes` as a static Pod or container.
2. In high-availability clusters, `multiple control plane nodes host` etcd instances, forming a distributed etcd cluster for redundancy and fault tolerance.
3. In managed Kubernetes clusters (like GKE, EKS, or AKS), the cloud provider manages etcd, and `users don't have direct access` to or control over its placement.

### How do you interact with ETCD cluster?
There are two command-line tools etcdctl and etcdutl to interact with ETCD cluster.
* Use etcdctl for managing the etcd cluster, performing key-value operations, and handling everyday tasks like backup and restore.
* Use etcdutl for advanced, low-level operations like defragmentation, validating database integrity, and recovering from corruption.

### Give sample etcdctl commands?
```
# Save a snapshot (backup)
etcdctl snapshot save /path/to/backup.db

# Restore a snapshot (restore)
etcdctl snapshot restore /path/to/backup.db

# Get a key from etcd
etcdctl get /key

# Put a key into etcd
etcdctl put /key "value"

# List etcd members
etcdctl member list

# Check etcd health
etcdctl endpoint health

```
### Give sample etcdutl commands?
```
# Defragment the etcd database
etcdutl defrag /path/to/database

# Validate the etcd database integrity
etcdutl validate /path/to/database

# Migrate etcd data
etcdutl migrate /source/path /destination/path

# Print etcd version
etcdutl version
```

### What is the default listening port of etcd?
`etcd` service listens on port 2379 by default.

### Where do we find all the information regarding etcd in our cluster?
```
cat /etc/kubernetes/manifests/etcd.yaml
```
### How do you create `etcd` snapshot for backup?
A snapshot may either be created from a live member with the etcdctl snapshot save command.
```
ETCDCTL_API=3 etcdctl --endpoints $ENDPOINT snapshot save snapshot.db
```
### How do you restore the `etcd` from snapshot?
```
etcdutl --data-dir <data-dir-location> snapshot restore snapshot.db
```
### How do you secure etcd?
To secure etcd, a distributed key-value store often used in Kubernetes clusters, we need to implement several security measures.

*  Enable encryption of data at rest by using `EncryptionConfiguration`.
*  Use `TLS` for authentication and encryption in transit.
```
--cert-file=/path/to/cert-file \
--key-file=/path/to/key-file \
--trusted-ca-file=/path/to/ca-file \
--client-cert-auth \
--peer-cert-file=/path/to/peer-cert-file \
--peer-key-file=/path/to/peer-key-file \
--peer-client-cert-auth \
--peer-trusted-ca-file=/path/to/peer-ca-file
```
* Enable Role-Based Access Control (RBAC) to restrict access to etcd.
* Backup regularly and test restore procedures to ensure data can be recovered in case of a security breach or system failure.
```
etcdctl snapshot save /path/to/backup.db
```
### What are etcd leases, and how are they used in Kubernetes?
Leases are used to manage temporary resources in etcd, such as session tokens or temporary storage. It is used to set time-to-live (TTL) for the keys.

> Leases provide a mechanism to lock shared resorces and coordinate activity between the members of a set.

## Conclusion
We covered the kubernetes etcd introduction and its basic.