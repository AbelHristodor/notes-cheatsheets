---
category: Configuration
Done: false
tags:
  - ckad
  - kubernetes
  - selectors/taints
order: 5
created: 2024-01-22T10:38
updated: 2024-01-31T17:22
---
# Taints and Tolerations
Taints and Tolerations are used to set restrictions on what pods can be scheduled on what nodes.

A taint can be applied on a one, only the pods having the toleration relative to the tain can be scheduled on that node.

## Taints
To apply a taint to a node use:
```bash
k taint nodes <node_name> <key>=<value>:<taint-effect>
```
The *taint-effect* section describes what will happen to the pod if they do not tolerate the taint. Can be one of:
- **NoSchedule**: pod should not be scheduled on the node
- **PreferNoSchedule**: try to avoid scheduling it on the node, but it's not guaranteed
- **NoExecute**: new pods will not be scheduled and already *existing pods* which do not tolerate the taint will be *evicted*

## Tolerations
Tolerations allow a pod to be scheduled on nodes with a specific *taint*.
To add tolerations to a pod add the *tolerations* key to the pod definition like so:
```yaml
...
spec:
  tolerations:
    - key: "<my_key>"
      operator: "Equal or Exists"
      value: "<value>"
      effect: "e.g. NoSchedule (see above)"
      
  containers:
    ...
```

Note the `"` on each of the value of the toleration section. They are mandatory since all values should be encoded.

**Best Practice**: the master should not have any application pods running. So it's best practice to add a taint `NoSchedule` to it.

## Node Selectors
Allow you to schedule pods onto nodes that have specific *labels*. E.g.  If i wanted to schedule pods only on nodes that have `size=large` as labels like this:
```yaml
...
spec:
  nodeSelectors:
    size: large
  containers:
    ...
```

So, the scheduler will schedule the pod only on the nodes having the specified label.
