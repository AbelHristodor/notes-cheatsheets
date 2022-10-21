*Kubectl CLI cheatsheet with most commond commands*

#kubernetes #kubectl #cheatsheet 

### Config
In order to write commands easier and faster, it is recommended to set up an alias. Open `.bashrc` and write the following:

```bash
alias k="kubectl"
```

Then, to apply the changes in the current terminal, run  `source .bashrc`.

**Multiple config files**
When working with multiple `kubeconfig` files, make sure to export them as ENV variables

```bash
export KUBECONFIG=~/.kube/kube-config-1.yml:~/.kube/kube-config-N.yml
```

## Management

### Cluster Management

|        Command         |                            Description                             |
|:----------------------:|:------------------------------------------------------------------:|
| `kubectl cluster-info` | Display endpoint info about the master and services in the cluster |
| `kubectl config view`  |                Get the configuration of the cluster                |

### Resource Management

| Command                                                         |                                                     Description                                                      |
|:--------------------------------------------------------------- |:--------------------------------------------------------------------------------------------------------------------:|
| `kubectl get all -A`                                            |                           Lists all resources from all namespaces (-A = --all-namespaces)                            |
| `k delete <resource> <resource_name> --grace-period=0 --formce` |                                             Force delete named resource                                              |
| `k get <resource> <resource_name>`                              | Returns general info of one resource. Add the `-o wide|json` flag for more info or to return the info in json format |
| `k describe <resource> <resource_name>`                         |                                          Returns all info about a resource                                           |
| `k get pod <pod_name> -o yaml > pod-definition.yaml`            |                              In order to extract the definition file of a pod/resource                               |
| `k edit pod <pod_name>`                                         |                                                 Edit pod through tty                                                 |

### Creation
| Command                 | Description                                                |
| ----------------------- | ---------------------------------------------------------- |
| `k create -f file.yaml` | Creates the defined resources of a file, imperative manner |
| `k apply -f file.yaml`  | Creates defined resources of a file, declarative manner    |
|                         |                                                            |
