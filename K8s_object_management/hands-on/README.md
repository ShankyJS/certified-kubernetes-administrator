## Working with Kubectl

````
kubectl get pods -n pods -o wide # This returns with more detail the pods.
````

````
kubectl get pods -o wide --sort-by .spec.NodeName # It can be filtered by json object structure.
````

````
kubectl get pods -o wide --selector component=etcd 
````

````
cloud_user@JhanSilva1c:~$ k get pods -n kube-system --selector k8s-app=calico-node
NAME                READY   STATUS    RESTARTS   AGE
calico-node-qk8qz   1/1     Running   4          13d
calico-node-txlwh   1/1     Running   4          13d
calico-node-wmxzq   1/1     Running   4          13d
cloud_user@JhanSilva1c:~$
````

````
kubectl describe pod my-pod # Returns human readable info, good for troubleshooting.
````

````
kubectl delete pod my-pod
````


