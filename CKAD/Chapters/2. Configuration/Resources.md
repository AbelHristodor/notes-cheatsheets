---
category: Configuration
Done: true
tags:
  - ckad
  - kubernetes
  - resources
order: 6
created: 2024-01-22T10:08
updated: 2024-01-22T10:36
---
# Resource Requirements
When deploying a pod on a node it requires some CPU and Memory to run. In k8s there are two metrics that allow the *scheduler* to understand if a pod can fit onto a node or if it should wait for a bigger node to deploy the pod: **requests** and **limits**.

**Requests** are the minimum resource the pod needs to have in order to run, so, the scheduler makes its decision to schedule or not a pod  based on the resources defined into the *requests* fields.
```yaml
...
spec:
  containers:
    - name: my_container
      resources:
	    requests: 
		  cpu: 1
		  memory: 2Gi
```
*CPU*: can be an `int` to indicate N vCpus (e.g. `cpu: 1` = 1 vCPU) or as a fraction using `m` e.g. (`cpu: 100m` = 0.1 vCPU)
*Memory*: `M, G, K` for `Megabytes` etc or `Mi, Gi, Ki` for `Mebibytes` etc.

But as said, *requests* indicate the *minum* resources a pod can use. So, if we don't give it limits it can consume all the resources of a node, which will suffocate the other pods on the node.

**Limits**
Specifies the maximum resources a pod can use.
```yaml
...
spec:
  containers:
    - name: my_container
      resources:
	    limits: 
		  cpu: 1
		  memory: 2Gi
```
If a pod tries to exceed the amount of specified resources some things can happen:
- **OOM**: pod consumes too much memory, it will be *terminated* with an error **OOMKilled** - Out of Memory Killed
- If the pod uses too much CPU the pod **won't** be killed but instead it will **throttle**

If *no requests* are specified k8s sets `requests = limits`.
If *no limits* pods can consume as much resources as available.

## Limit Ranges
Limit ranges allow setting default limits for containers and pods that are created without requests or limits. They are valid at a namespace level.
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-resource-constraint
spec:
  limits:
  - default: # this section defines default limits
      cpu: 500m # same for memory - memory: 1Gi
    defaultRequest: # this section defines default requests
      cpu: 500m
    max: # max and min define the limit range
      cpu: "1"
    min: # request 
      cpu: 100m
    type: Container
```

## ResourceQuotas
Sets **hard** resource limits  for entire namespaces allowing to define how much memory & cpu a namespace can consume at maximum.
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
	name: pods-high
spec:
	hard:
		requests.cpu: "1000" # Max requests
		limits.memory: 200Gi # Max Gi used by the ns
		pods: "10" # Max number of pods
```