Introduction to kubernetes namespaces

#namespaces #kubernetes #kubectl 

# Namespaces
Namespaces allow us to separate things between different environments.
By default k8s created a few namespaces `kube-system`, `default` and `kube-public` which contains resources that should be accessible by all resources in all namespaces.

Each namespace can have different CPU/Memory quotas.
Each resource can reach another resource in the same namespace by using its simple name. If a resource needs to reach another resource in a different namespace, it should reach it by `<service>.<namespace>.<service_type>.cluster.local`

## Resource Quotas
Resource quotas define how much CPU/Memory a namespace can use. 

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
	name: compute-quota
	namespace: dev
spec:
	hard:
		pods: 10
		requests:
			cpu: 4
			memory: 5Gi
		limits:
			cpu: 10
			memory: 10Gi
```