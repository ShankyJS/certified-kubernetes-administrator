# Working with Kubectl

Kubectl is the command line tools that allows you to interact with the K8s api, you can use kubectl to deploy applications, inspect and manage cluster resources and view logs.

## Kubectl get

Can be used to list objects in the Kubernetes Cluster.


-o Set output format.
--sort-by Sort outputs using a JSONPath expression.
--selector -- Filter results by label.

````
kubectl get <object> <object name> -o <output-type> --sort-by <JSONPATH> --selector <selector>
````

## Kubectl describe

You can get detailed information about Kubernetes objects using k describe.

````
k describe <object-type> <object-name>
````

## Kubectl create

Used to create objects, you can supply a object with YAML using -f.

````
kubectl create -f <file-name>
````

## Kubectl apply

Kubectl apply is similar to kubectl create, however if you use kubectl apply it will try to modify the file if there is something different, so you can use k apply to create or modify objects.

## Kubectl delete

Deletes objects.

````
kubectl delete <type-object> <objectname>
````

## Kubectl exec

Exec can be used to run commands inside of your container, keep in mind that in order for a command to succeed the necessary software must exist within the container to run it.

kubectl exec <pod name> -c <container-name> -- <commamnd>
