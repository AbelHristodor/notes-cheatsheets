---
category: Core
Done: true
tags:
  - ckad
  - kubernetes
order: 1
created: 2024-01-21T12:25:00
updated: 2024-01-21T19:52
---
# Cluster
Is a set of nodes where, when one node fails, the other nodes take up the load. So, having multiple nodes also helps sharing workload.
## Nodes
Physical machines used to make up a cluster. They can be one of two types:
- **worker nodes**
- **master nodes**
### Worker
Machine, physical or virtual where *kubernetes* is installed. It is a worker machine so it will contain your running application.
If your application goes down, it is better to have more than one node in order to implement zero-downtime or HA (High-Availability) in your cluster.

They have the *kubelet-agent* that is responsible of communicating to the master node and do what the master says.
### Master
Is another node that is responsible of the orchestration of the nodes running on the cluster. It is the only node that has running inside the *kube-apiserver*, *etcd*, *controller*, *API scheduler*.
# Components
When installing k8s on a system, you actually install multiple components:
- [[#API Server]]
- [[#Etcd]]
- [[#Kubelet]]
- [[#Container Runtime]]
- [[#Controller]]
- [[#Scheduler]]

### API Server
Is the frontend for k8s. The users, CLIs such as `kubectl` (See [[Kubectl Cheatsheet]]) etc.. all interact w/ API Server in order to talk to k8s or the application installed in it.

### Etcd
It is a key-value store that holds all necessary information about nodes, master(s) and makes sure, by implementing locks that there are no conflicts between masters when there are more than one.

### Scheduler
It is responsible for distributing work or containers to different nodes. It looks for newly created containers and then it assigns them to different nodes or pods.

### Controller
Is the brain behind orchestration. It is responsible for understanding when nodes/pods/containers go down or need to be created and responds accordingly.

### Container Runtime
Software that allows to run our application in a containerized way. E.g. [Docker](www.docker.com), containerd or others.

### Kubelet
It is the agent running in each node and it is responsible of making sure containers are running as expected on the nodes. Also it communicates with the *kube-apiserver* on the master node sharing other information such as *status*, *health* and other which are all stored on the etcd in the master node.

![[K8s_Architecture_2.png|Kubernetes architecture.]]
<p align="center" style="font-style: italic">Kubernetes general architecture</p>


**Next:** [[Env, ConfigMaps, Secrets]]