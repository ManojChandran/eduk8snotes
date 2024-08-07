# Introduction 
Let's discuss about health check, it's importance and implementation in Kubernetes.

### What is a health check in Kubernetes?
In Kubernetes, a health check refers to the mechanism used to determine the health and operational status of containers within Pods. Health checks are essential for maintaining the reliability, availability, and proper functioning of applications running in a Kubernetes cluster.

### What are Kubernetes Probes used for? 
Kubernetes Probes are used for determining health and readiness of container inside a POD.

### What are the different types of Probes?
There are mainly three types of Probes 
Liveness Probe -  container 
Readiness Probe - container network 
Startup Probe - application inside container 

### What is a liveness probe?
A liveness probe in Kubernetes is a mechanism used to determine if a container inside a Pod is still running. Liveness probes determine when to restart a container.

### What is a Readiness probe?
A Readiness Probe in Kubernetes is used to determine if a container within a Pod is ready to serve traffic. If the readiness probe fails, Kubernetes will remove the container from the list of endpoints for the service, ensuring that no traffic is sent to the container until it becomes ready again.

### What is a startup probe?
A Startup Probe in Kubernetes is used to determine whether an application within a container has started successfully.

### What are the types of probe?
Kubernetes supports three types of liveness probes:
* HTTP Get probe
* TCP Socket probe
* EXEC probe

### Where is liveness probe configured?
Liveness probes are configured in the Pod specification.

### Give an example manifest file for HTTP probe?
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: readiness-pod
spec:
  containers:
  - name: myapp
    image: myapp:latest
    readinessProbe:
      httpGet:
        path: /ready
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 5
```

### Give an example manifest file for TCP Socket?
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: readiness-tcp-pod
spec:
  containers:
  - name: myapp
    image: myapp:latest
    readinessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 5
```

### Give an example manifest file for EXEC Socket?
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: readiness-exec-pod
spec:
  containers:
  - name: myapp
    image: myapp:latest
    readinessProbe:
      exec:
        command:
        - cat
        - /tmp/ready
      initialDelaySeconds: 5
      periodSeconds: 5
```

### What are the major components of liveness probe?
* initialDelaySeconds: Time to wait before performing the first probe after the container has started.
* periodSeconds: Time interval between subsequent probes.
* timeoutSeconds: Maximum duration for a probe to complete.
* successThreshold: Minimum consecutive successes for the probe to be considered successful after it fails.
* failureThreshold: Minimum consecutive failures for the probe to be considered failed after it succeeds.

### What are the benifits of Probe?
Automatic recovery 
Detecting deadlock
Resilience and self healing

### Who restarts container for Kubernetes?
Kubelet: The agent that runs on each node in the cluster. It ensures that containers are running in a Pod and restarts them if they fail according to the defined policy.

### Can we use all three probes together in a POD?
Yes, we can use all three probes (liveness, readiness, and startup probes) together in a Pod.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: example-pod
spec:
  containers:
  - name: myapp
    image: myapp:latest
    
    # Startup Probe
    startupProbe:
      httpGet:
        path: /startup
        port: 8080
      initialDelaySeconds: 10
      periodSeconds: 5
      failureThreshold: 30
    
    # Liveness Probe
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 45
      periodSeconds: 10
    
    # Readiness Probe
    readinessProbe:
      httpGet:
        path: /ready
        port: 8080
      initialDelaySeconds: 30
      periodSeconds: 5
```

## Conclusion
We learned about the kubernetes Probes and its implementation.