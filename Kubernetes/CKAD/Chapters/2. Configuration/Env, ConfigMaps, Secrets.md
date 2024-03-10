---
category: Configuration
Done: true
tags:
  - ckad
  - kubernetes
  - pod
  - configmap
  - secrets
order: 4
created: 2024-01-11T15:04
updated: 2024-01-21T19:52
---
# Pod
## Command & Args
When defining a [[Cluster#^af1a14|pod]] like this:
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
      command: ["my_command"]
      args: ["my_args", "3"]
```

you can also define some parameters like *command* and *args* to override the *entrypoint* and the *cmd*  statements from the docker image definition.
That means that in your Pod definition you can pass:
- `command`:  to override the `ENTRYPOINT` statement of the Dockerfile
- `args`: to override the `CMD` statement of the Dockerfile

**Remember**:  in docker, `CMD` gets overridden in `docker run <image> <my_command>`  by the `<my_command>` , but you cannot ovverride the `ENTRYPOINT`.

## Environment Variables
Env variables can be defined in multiple ways, the simples is by using the `env` key in the container configuration.
```yaml
spec:
	containers:
		- name: nginx
		  env:
			- name: MY_VAR
			  value: my_value
```
Also it can be populated from a ConfigMap or a Secret
```yaml
spec:
	containers:
		- name: nginx
		  env:
			- name: MY_VAR
			  valueFrom:
				  configmapKeyRef: # or secretKeyRef
```

# ConfigMap
Are used to store key-value pair data to be later passed to pods/deployments/other objects. As seen above they can be injected as env vars.
There are 2 steps in using configmaps:
## Creation
Imperative way:
1. Directly: `k create configmap <name> --from-literal=<key>=<value> --from-literal=...`
2. From a file: `k create configmap <name> --from-file=<path-to_file>`

Declarative way:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
	name: my_name
data:
	MY_VAR: my_value
```
## Injection
To inject an entire configmap as env vars simply use the following
```yaml
envFrom:
 - configMapRef:
	 name: my_config_map
```
To inject one env var at the time use
```yaml
env:
	- name:
	  valueFrom:
		  configMapKeyRef:
			  - name: my_config_map
			    key: MY_VAR
```

# Secrets
Allows to hide sensitive information that can be used by pods/objects. It is similar to a configmap but  its contents are hidden. They are not *encrypted*, not even in etcd, just *encoded*. You should be using a proper secrets manager from aws, gcp, azure or hashicorp vault.

## Creation
```
k create secret generic <name> --from-literal=<key>=<value> #or --from-file=<path-to-file>
```
Or 
```yaml
apiVersion: v1
kind: Secret
metadata:
	name: my_name
data:
	MY_VAR: encoded_value
```
You should encode data before saving. You can achieve so by doing:
`echo -n "my_value" | base64`

To decode `echo -n "my_encoded" | base64 -d`
## Injection
To inject an entire configmap as env vars simply use the following
```yaml
envFrom:
 - secretRef:
	 name: mysecret
```
To inject one env var at the time use
```yaml
env:
	- name:
	  valueFrom:
		  secretMapKeyRef:
			  - name: my_secret
			    key: MY_VAR
```
To inject as a volume
```yaml
volumes:
- name: my_secret_volume
  secret:
    secretName: my_secret
```



**Next:** [[3. Multi-Container]]