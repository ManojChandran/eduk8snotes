# Introduction 
Last chapter's we discussed about the etcd, where our objects are stored. This chapter let try learn about services, which  exposes the pods created.

### What is a service?
A service is a method for exposing a network application that is running as one or more Pods in our cluster.

### What does the service Do?
Service identify the semantic set of resources(Pods) associated with them using Labels and Selectors.

### What is the key benifit of using service?
It decouples the workloads by abstracting the communication.

### How does the service expose the Pods?
A service provides a stable IP address and DNS Name to route the traffic to thr Pods, even as theor individual IP address is changed.

### How does a Service discover Pods in Kubernetes?
Kubernetes Services use label selectors and EndPoints to discover and route traffic to the correct set of Pods. The discovery process follows these key steps:
* Label Selectors → Match Pods dynamically
* Endpoints Object → Stores actual Pod IPs
* Cluster DNS → Provides a resolvable name for the Service
* kube-proxy → Handles traffic routing and load balancing

### What are the different types of Services in Kubernetes?
* ClusterIP - Exposes the Service internally within the cluster, Use it for internal microservices.
* NodePort - Exposes the Service externally on a static port on each cluster Node, Use it for direct access via a Node’s IP.
* LoadBalancer - Provisions an external Load Balancer (only works in cloud environments), Use it for cloud-based external access.
* ExternalName - Maps a Service to an external DNS name (instead of selecting Pods).Use it to redirect traffic to external services.

### What is the default type of a Kubernetes Service?
ClusterIP

### How does Kubernetes load balance traffic across Pods in a Service?
|Load Balancing Type	|Mechanism	|When to Use?
|-----------------------|-----------|--------------|
|ClusterIP	|Round-robin via kube-proxy	|Internal communication between Pods
|NodePort	|Round-robin via kube-proxy	|Direct access via Node’s IP (testing)
|LoadBalancer	|Cloud provider's LB + NodePort	|Exposing services externally
|Ingress Controller	|Reverse proxy (NGINX, Traefik)	|Advanced routing & SSL termination

### What is the role of kube-proxy in Kubernetes networking?
`kube-proxy` is a networking component in Kubernetes that manages network traffic routing to ensure communication between Services and Pods. It runs on each node in the cluster and maintains network rules to allow efficient load balancing and service discovery.

To check whether kube-proxy is using iptables or IPVS:
```sh
% kubectl get pods -n kube-system -l k8s-app=kube-proxy
NAME               READY   STATUS    RESTARTS   AGE
kube-proxy-cmjcm   1/1     Running   0          5m21s
kube-proxy-gb998   1/1     Running   0          5m18s
kube-proxy-l5fzh   1/1     Running   0          5m18s
% kubectl logs -n kube-system kube-proxy-l5fzh | grep "Using"                                                
I0327 07:52:45.281246       1 server_linux.go:170] "Using iptables Proxier"
```

### Can a Service work without kube-proxy? What alternatives exist?
Yes, a Kubernetes Service can work without kube-proxy, but an alternative networking solution is required to handle service-to-pod traffic routing.
By default, kube-proxy manages service-to-pod traffic using iptables, IPVS, or user-space proxying, but some `CNI (Container Network Interface) plugins` and `service mesh solutions` can replace it.

### Can a Service route traffic to multiple deployments? How?
Yes, A Service selects Pods based on labels. If multiple Deployments create Pods with matching labels, the Service will distribute traffic across all those Pods, regardless of which Deployment created them.

Check if the Service is selecting Pods from both Deployments:
```sh
kubectl get endpoints my-service
```

### What happens if a Pod fails? Will the Service automatically update its endpoints?
Yes, Kubernetes Services automatically update their endpoints when a Pod fails. The Service continuously monitors the availability of Pods and ensures traffic is only routed to healthy Pods.

### Can a Service span multiple namespaces? How can we achieve cross-namespace service discovery?
No, a Kubernetes Service is limited to a single namespace by default. It can only discover and route traffic to Pods within the same namespace.

However, cross-namespace service discovery can be achieved using external services, `DNS resolution`, or `ServiceExport` (in multi-cluster setups).

### What is EndpointSlice?
An EndpointSlice is an API resource in Kubernetes that stores network endpoints (IP addresses and ports) for a Service. It provides a scalable and efficient way to track and distribute endpoint information across a cluster.

Before Kubernetes 1.17, Kubernetes used the Endpoints (v1.Endpoints) API to store all endpoints of a Service in a single object.
* This approach worked fine for small clusters, but it caused performance issues when Services had a large number of endpoints.
* EndpointSlice solves this by distributing the endpoints across multiple smaller objects, each containing a subset of the endpoints.
> In the latest Kubernetes versions (starting from Kubernetes 1.21 and beyond), EndpointSlice is the default mechanism for tracking Service endpoints.
```sh
kubectl get endpointslice -n kube-system
```
### Can we apply Network policy on the service we create?
No, Network Policies in Kubernetes are applied to Pods, not directly to Services. However, since Services route traffic to Pods, we can control which Pods can receive or send traffic by applying Network Policies.

### Why Can’t We Apply a Network Policy to a Service?
* A Service is just an abstraction that provides a stable IP and DNS name for a group of Pods.
* Network Policies apply at the Pod level, using labels to select Pods.
* The Service itself does not handle traffic; kube-proxy routes requests to the actual Pods.

### How do you check the IP address assigned to a Service?
1. Find Selected Pods Using Label Matching
```sh
kubectl get pods -l app=my-app
```
2. Check Endpoints Manually
```sh
kubectl get endpoints my-service -o yaml
```

## Conclusion
We covered the kubernetes `service` introduction and its basic.
