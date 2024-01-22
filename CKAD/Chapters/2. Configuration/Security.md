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
updated: 2024-01-21T19:52
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