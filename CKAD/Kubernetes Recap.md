*General Kubernetes architecture recap*

#kubernetes #kubectl #architecture

## Node (Worker)
Machine, physical or virtual where kubernetes is install. It is a worker machine so it will contain your running application.

If your application goes down, it is better to have more than one node in order to implement zero-downtime or HA (High-Availability) in your cluster.

## Cluster
Is a set of nodes where, when one node fails, the other nodes take up the load. So, having multiple nodes also helps sharing workload.

## Master Node
Is another node that is responsible of the orchestration of the containers running on the node. It also manages all nodes.

# Components
When installing k8s on a system, you actually install multiple components:
- API Server
- Etcd
- Kubelet
- Container Runtime
- Controller
- Scheduler

## API Server
Is the frontend for k8s. The users, CLIs such as `kubectl` (See [[Kubectl Cheatsheet]]) etc.. all interact w/ API Server in order to talk to k8s or the application installed in it.

## Etcd
It is a key-value store that holds all necessary information about nodes, master(s) and makes sure, by implementing locks that there are no conflicts between masters when there are more than one.

## Scheduler
It is responsible for distributing work or containers to different nodes. It looks for newly created containers and then it assigns them to different nodes or pods.

## Controller
Is the brain behind orchestration. It is responsible for understanding when nodes/pods/containers go down or need to be created and responds accordingly.

## Container Runtime
Software that allows to run our application in a containerized way. E.g. [Docker](www.docker.com) 

## Kubelet
It is the agent running in each node and it is responsible of making sure containers are running as expected on the nodes. Also it communicates with the *kube-apiserver* on the master node sharing other information such as *status*, *health* and other which are all stored on the etcd in the master node.

![[K8s_Architecture_2.png|Kubernetes architecture.]]
<p align="center" style="font-style: italic">Kubernetes general architecture</p>
# Pods
Containers are encapsulated in a k8s object known as *pod*. The smallest object you can create in K8s.

![[Pod.png]]

Pods allow you to scale on the same node or more nodes in order to handle the upcoming traffic. The only way you can scale is by adding more pods and not by duplicating containers in pod. A pod can have multiple containers, usually not by the same kind; sometimes a pod can have a main container and other containers that *help* (known as *helper*) that exists only as long as the main container lives. They usually share the same storage space. 

#### Pod as Yaml
Pods can be defined as yaml files.

For example:
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
| `kind`       | Can be of type Pod, Service, ReplicaSet, Deployment and other custom resources      |
| `metadata`     | Set metadata values, only keys that k8s expects and nothing else.                   |
| `name`         | Pod name                                                                            |
| `labels`       | Dictionary that can have any key-value pairs. E.g. labels can be used to group pods |
| `spec`         | Specification dictionary containing settings for the pod (or other resources)                                                                                    |
