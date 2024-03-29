---
category: Core
Done: true
tags:
  - pod
  - deployment
  - replicaset
  - namespace
order: 2
created: 2024-01-21T19:41
updated: 2024-01-21T19:52
---
# Pods
Containers are encapsulated in a k8s object known as *pod*. The smallest object you can create in K8s representing a single instance of your application.

![[Pod.png]]

Pods allow you to scale on the same node or more nodes in order to handle the upcoming traffic. The only way you can scale is by adding more pods and not by duplicating containers in pod. A pod can have multiple containers, usually not by the same kind; sometimes a pod can have a main container and other containers that *help* (known as *helper*) that exists only as long as the main container lives. They usually share the same storage space and are all on the same network. 

#### Pod as Yaml
Pods can be defined as yaml files.
For example: ^af1a14
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
    - name: nginx-container
      image: nginx:<version|tag>
```

| Key          | Description                                                                         |
| ------------ | ----------------------------------------------------------------------------------- |
| `apiVersion` | Version of the api of reference                                                     |
| `kind`       | Can be of type *Pod, Service, ReplicaSet, Deployment* and other custom resources      |
| `metadata`     | Set metadata values, only keys that k8s expects and nothing else.                   |
| `name`         | Pod name                                                                            |
| `labels`       | Dictionary that can have any key-value pairs. E.g. labels can be used to group pods |
| `spec`         | Specification dictionary containing settings for the pod (or other resources)                                                                                    |

# ReplicaSet
A *replication controller* is used when we want to have more replicas (instances) of the same pod, so if one fails we can still have other instances of our application running. Thus it provides high-availability. 
It is good practice to use a *replication controller* even if you're defining just a single pod with one replica since its *replication controller* ensures that there's always a single pod running, thus, achieving high-availability by restarting the pod when it crashes.

Note: *replication controller* is the older tecnology. Now the new way of implementing replication is achieved by using the **ReplicaSet**. All above is still valid for the newer technology.

In order to let know what pod to *replicate*, we must define a `template` into the replica controller for it to know how the pod replicated should look like.

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
	name: myapp-rc
	labels: 
		app: myapp
		type: frontend
spec:
	template:
		metadata:
			name: myapp-pod
			labels:
				app: myapp
				type: frontend
		spec:
			containers:
				- name: nginx
				  image: nginx
	replicas: 3
```

To manage it you can retrieve the object: `k get replicationcontroller`

Let's now check the **ReplicaSet**
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
	name: myapp-rc
	labels: 
		app: myapp
		type: frontend
spec:
	template:
		metadata:
			name: myapp-pod
			labels:
				app: myapp
				type: frontend
		spec:
			containers:
				- name: nginx
				  image: nginx
	replicas: 3
	selector:
		matchLabels:
			type: frontend
```
As you can see the main difference is the presence of the `selector` key. The *selector* keys allows us to define what pods should fall into the *replicaset* domain i.e. what pods the **rs** should have control over. This is because a **rs** can control pods that weren't created by the **rs** but have the correct labels. E.g. you can create a *rs* that monitors already pre-created pods. The `template` definition section is *mandatory* because, in case one of the pre-created pods dies, the *rs* must have a way of recreating it.

To manage it you can retrieve the object: `k get replicaset`

### Labels & Selectors
Why do we need to have labels and selectors in k8s?
In order to understand what *pods* a *replicaset* should monitor, it needs someway of *finding* and *filtering* them. We use `labels` to group pods and so *select* them using the *selector*.

### Scaling
In order to *increase* or *decrease* the number of pods (*replicas*) of a **replicaset**, there are two ways: 
- `declarative`way where you change the file definition of the rs and then apply it
- `imperative` by using this command `k scale --replicas=<REPLICAS> replicaset <NAME>`. This won't change the file definition.

You can also make *rs* scale based on load. That's called *horizontal scaling*. 

# Deployment
 A deployment is a higher order component than replicasets. It allows for  pods to be updated/managed using **rolling updates**, so it allows to upgrade, undo changes, pause and resume changes as required.
 ![[Deployment.png]]

The file is very much similar to the `replicaset` one. This is because the `deployment` creates a `replicaset` which then creates `pods`.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: my-depl
	labels: 
		app: myapp
		type: frontend
spec:
	template:
		metadata:
			name: myapp-pod
			labels:
				app: myapp
				type: frontend
		spec:
			containers:
				- name: nginx
				  image: nginx
	replicas: 3
	selector:
		matchLabels:
			type: frontend
```


# Namespace
Namespaces allow us to separate things between different environments.
Kubernetes on startup creates 3 namespaces by default:
- *kube-system* - where system resources are created
- *default* - default empty ns
- *kube-public* - where resource available to all users should be created

Each namespace can have different CPU/Memory quotas called **resource quotas**.

Each resource can reach another resource in the same namespace by using its simple name. If a resource needs to reach another resource in a different namespace, it should reach it by `<service>.<namespace>.<type>.cluster.local` e.g. `my_db.dev.svc.cluster.local` .
This happens because k8s creates a *dns entry* automatically for each service, in fact the *cluster.local* is the **base domain** of the cluster.

To run commands in a different namespace just append `-n <my_ns>` to pretty much any command or add a `namespace: <my_ns>` tag under the `metadata` object.

```yaml
apiVersion: v1
kind: Namespace
metadata:
	name: dev
```

To switch to a `namespace` *permanently* run:
`k config set-context $(k config current-context) -n <my_ns>` 
now, every command will be run under the `<my_ns>` namespace.

To view pods in *all namespaces* run the command with  `--all-namespaces`.
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
