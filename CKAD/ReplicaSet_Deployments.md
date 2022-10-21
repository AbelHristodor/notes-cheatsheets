They are processes that monitor k8s objects and respond accordingly.

#kubernetes #kubectl #k8s 

# Replication Controller

The replication controller are used to achieve High Availability, they are the ones that allow us to run multiple instances of a pod in a cluster. You can use a Replication Controller also with a single pod, it will ensure the pod will always be running (be it one or 100). 
It is also used for sharing load between pods (load-balancing), in fact the Replication Controller live across multiple nodes between the cluster in order to achieve HA and Load-Balancing.

#### Replication Controller vs ReplicaSet
The replication controller is an older technology being replaced by the replicaset. ReplicaSet is the new recommended way of setting up replication.

##### Replication Controller YAML
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    name: myapp
    type: front-end
spec:
	replicas: 1
	template:
	## POD
		metadata:
			name: myapp-pod
			labels: myapp
			type: frontend-pod
		spec:
			containers:
			 - name: nginx-container
				 image: nginx
```

##### ReplicaSet
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
	name: myapp-rs
	labels:
		name: myapp
		type: frontend
spec:
	selector:
		matchLabels:
			type: frontend
	replicas: 3
	template:
		metadata:
			name: myapp-pod
			labels: myapp
			type: frontend-pod
		spec:
			containers:
			 - name: nginx-container
				 image: nginx
```
Why `selector` field? Because it can handle pods that aren't directly created by the replicaset. E.g. pods created before implementing the replicaSet. It is not mandatory to set it.

## Labels and Selectors
Labels allow ReplicaSet to understand which pods to monitor. 

# Deployments
A deployment allows us to scale, to reach HA in our cluster, to roll updates/downgrades all within one single resource. It basically is an upgraded version of ReplicaSet. In fact when creating a new deployment, it also creates a ReplicaSet.

Example:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: myapp-deploy
	labels:
		name: myapp
		type: frontend
spec:
	selector:
		matchLabels:
			type: frontend
	replicas: 3
	template:
		metadata:
			name: myapp-pod
			labels: myapp
			type: frontend-pod
		spec:
			containers:
			 - name: nginx-container
				 image: nginx
```