---
category: Configuration
Done: 
tags:
  - ckad
  - kubernetes
  - security
  - service-accounts
order: 5
created: 2024-01-21T19:50
updated: 2024-01-22T09:41
---
# SecurityContexts
A security context defines privilege and access control settings for a Pod or Container. Container settings are privileged compared to Pod-level security contexts. By running a pod without a *security context* it will run as *root* user as default.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  containers:
  - name: sec-ctx-demo
    image: busybox:1.28
    command: [ "sh", "-c", "sleep 1h" ]
    securityContext:
	  capabilities:
		  add: ["MAC_ADMIN"] # Add other capabilities here -- linux -- only supported at container-level
      allowPrivilegeEscalation: false
```

# ServiceAccounts
A service account is an account that can be used by an application/external software to interact with the cluster while having specific permissions. It is like a `user` account but for machines/softwares.

To create one: `k create serviceaccount <name>` 
Once created, the service account comes with a *token* that must be used by the external app while authenticating with the cluster. The token is stored as a secret object linked to the `service account`. To view  it use the `k describe secret <secret>` command.