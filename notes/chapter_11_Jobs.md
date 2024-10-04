# Introduction 
Last chapter we discussed about the workload managements object `daemonSet`. In this chapter,  we will learn in detail on  workload `JOBs` management object.

### What are JOBs in Kubernetes?
A Kubernetes Job is a resource object that ensures a specified number of pods successfully complete a particular task. Unlike Deployments, which are designed to keep applications running indefinitely, Jobs are intended for tasks that have a clear start and end.

### Write up a sample Kubernetes JOB?
```yaml
Manifest file:
apiVersion: batch/v1
kind: Job
metadata:
  name: demo-job
spec:
  completions: 3
  parallelism: 2
  template:
    spec:
      containers:
      - name: example
        image: busybox
        command: ["echo", "Hello JOB"]
      restartPolicy: Never
```
## How to Start, Suspend, Resume and Stop Kubernetes JOB?
* Start a Job: `kubectl apply -f job.yaml`.
* Suspend a Job: Edit the Job spec and set `spec.suspend` to true.
* Resume a Job: Edit the Job spec and set `spec.suspend` to false.
* Stop/Delete a Job: kubectl delete job <job-name>.
* Restart a Failed Job: Delete and reapply the Job.

### What happens, when Kubernetes jobs are suspended?
When a Kubernetes Job is suspended, its execution is paused, meaning that:

1. Pod Creation Stops
2. Running Pods Remain Active
3. Job is in a Paused State
                
### What are the types of JOBs in Kubernetes?
1. Non-parallel jobs: Runs a single task to completion
2. Multiple parallel jobs: Large batches JOBS
3. Parallel jobs with fixed number of completions: Targetted for a specified number of tasks completion

### How do you run the JOB in parallel?
To run the JOB in parallel: Edit the Job spec and set `spec.parallelism` to number of parallel instance of JOB run you need.
```yaml
kind: Job
metadata:
  name: demo-job
spec:
  parallelism: 2
```

### Does the Kubernetes retry automatically to complete a failed JOB?
Yes, Kubernetes retry automatically by restarting the failed JOB. We can restrict the retry by setting `.spec.backoffLimit` to the number of retry we need Kubernetes to retry (default value is 6).

### How to clean up finished JOB?
We can configure a Job or CronJob to automatically delete its finished Jobs by setting the `.spec.ttlSecondsAfterFinished` field.

### What Happens when a Kubernetes Job Fails?
### What are the things to Check Before Re-running a failed Job?
### How to check the JOB status?


## Conclusion
We covered the kubernetes JOB's, as part of the work load management.