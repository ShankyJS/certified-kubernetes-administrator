# What is draining?

When performing maintenance, you may sometimes need to remove a Kubernetes node from service.

To do this, you can drain the node Containers running on the node will be gracefully terminated and potentially rescheduled on another node.

To do that:

````
kubectl drain <node name> 
````

## Ignoring DaemonSets

When draining a node, you may need to ignore DaemonSets (pods that are tied to each node). If you have any DaemonSet pods running on the node, you will likely need to use the --ignore-daemonsets flag.

````
kubectl drain <node> --ignore-daemonsets
````

## Uncordoning a Node

If the node remains part of the cluster you can allow pods to run on the node again when maintenance is complete using the kubectl uncordon command.

````
kubectl uncordon <node>
````

## Practice

So we created a single pod without any deployment and also a deployment with 2 nginx pods attached to it.

And when we tried to run drain on one node we got the next message:

````
node/jhansilva3c.mylabserver.com cordoned
error: unable to drain node "jhansilva3c.mylabserver.com", aborting command...

There are pending nodes to be drained:
 jhansilva3c.mylabserver.com
cannot delete Pods not managed by ReplicationController, ReplicaSet, Job, DaemonSet or StatefulSet (use --force to override): default/my-pod
cannot delete DaemonSet-managed Pods (use --ignore-daemonsets to ignore): kube-system/calico-node-wmxzq, kube-system/kube-proxy-shmnm
````

This is essentialy happening for two reasons, the first one is because drain can only move pods that are managed my ReplicaSets, jobs, DaemonSets or StatefulSets, because we created this pod without any of them is not able to move it, and because cordon doesn't want to delete the pods and probably outage or service is sending that issue.

The second error is because the pods that are managed by DaemonSets and are tied just to the node can't be deleted without the flag --ignore-daemonsets.


````
k drain jhansilva3c.mylabserver.com --ignore-daemonsets --force
node/jhansilva3c.mylabserver.com already cordoned
WARNING: deleting Pods not managed by ReplicationController, ReplicaSet, Job, DaemonSet or StatefulSet: default/my-pod; ignoring DaemonSet-managed Pods: kube-system/calico-node-wmxzq, kube-system/kube-proxy-shmnm
evicting pod default/my-pod
evicting pod default/my-deployment-5f85c44867-wqngz
````

We also used the --force flag (don't use this one if you are in a situation when you can't lose your pods).


````
cloud_user@JhanSilva1c:~/Documents$ k get nodes
NAME                          STATUS                     ROLES                  AGE     VERSION
jhansilva1c.mylabserver.com   Ready                      control-plane,master   7d23h   v1.20.1
jhansilva2c.mylabserver.com   Ready                      <none>                 7d23h   v1.20.1
jhansilva3c.mylabserver.com   Ready,SchedulingDisabled   <none>                 7d23h   v1.20.1
````

````
cloud_user@JhanSilva1c:~/Documents$ k uncordon jhansilva3c.mylabserver.com
node/jhansilva3c.mylabserver.com uncordoned
````

The uncordon will not re-balance the loads.
