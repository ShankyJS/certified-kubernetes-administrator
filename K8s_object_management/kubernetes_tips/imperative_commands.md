# Imperative commands

Declarative:

Define objects using data structures such as YAML or JSON.

Imperative: 
Define objects using kubectl commands and flags. Some people find imperative commands faster. Experiment and see what works for you.
Ie.

````
kubectl create deployment my-deployment -- image=nginx
````

# Quick Sample YAML.

Using the --dry-run flag to run an imperative command without creating an object. Combine it without -o yaml to quickly obtain a sample YAML file you can manipulate.

````
k create deployment my-deployment --image=nginx --dry-run -o yaml
````

# Record a Command.

Use the --record flag to record the command that was used to make a change.

````
kubectl scale deployment my-deployment --replicas=5 --record
````

# Use the docs.

You can often find YAML examples in the K8s documentation. You are allowed to use this documentation during the examen. Feel free to copy and paste YAML and/or commands from the docs.

````
 k create deployment nginx-deployment --image=nginx --dry-run=client --replicas=5 -o yaml > nginx-deployment.yaml
````
