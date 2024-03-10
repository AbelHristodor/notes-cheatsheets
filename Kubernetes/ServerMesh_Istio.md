---
created: 2024-03-10T10:13
updated: 2024-03-10T10:30
category: Management
tags:
  - service-mesh
  - networking
---
# Service Mesh
A service mesh manages communication between *microservices*. 
A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term “service mesh” describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.  More [here.](https://istio.io/latest/about/service-mesh/)

# Istio
Istio is an open-source service **mesh implementation** that layers onto existing distributed applications. Istio is the path to <ins>load balancing, service-to-service authentication, and monitoring </ins>– with few or no service code changes. 
Its powerful control plane brings vital **features**, including:
- Secure *service-to-service communication* in a cluster with TLS encryption, strong identity-based authentication and authorization
- *Automatic load balancing* for HTTP, gRPC, WebSocket, and TCP traffic
- Fine-grained *control of traffic* behavior with rich routing rules, retries, failovers, and fault injection
- A *pluggable policy layer* and configuration API supporting access controls, rate limits and quotas
- *Automatic metrics, logs, and traces* for all traffic within a cluster, including cluster ingress and egress

## How it works
Istio has two components: the **data plane** and the **control plane**.

![[Istio.png]]