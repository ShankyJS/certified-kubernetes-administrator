# Upgrading with kubeadm

When using Kubernetes, you will likely want to periodically upgrade Kubernetes to keep your cluster up to date.

## Control Plane Upgrade Steps

- Upgrade kubeadm on the control plane node.
- Drain the control plane node.
- Plan the upgrade (kubeadm upgrade plan).
- Apply the upgrade (kubeadm upgrade apply).
- Upgrade kubelet and kubectl on the control plane node.
- Uncordon the control plane node.

## Worker node Upgrade Steps

- Drain the node
- Upgrade kubeadm
- Upgrade the kubelet configuration (kubeadm upgrade node)
- Upgrade kubelet and kubectl
- Uncordon the node

## Hands on Demo

### Control plane upgrade

First we have to check the versions that we have on all the nodes:

````
cloud_user@JhanSilva1c:~$ k get nodes
NAME                          STATUS                     ROLES                  AGE   VERSION
jhansilva1c.mylabserver.com   Ready                      control-plane,master   8d    v1.20.1
jhansilva2c.mylabserver.com   Ready,SchedulingDisabled   <none>                 8d    v1.20.1
jhansilva3c.mylabserver.com   Ready                      <none>                 8d    v1.20.1
````

Now we can update kubeadm:

````
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubeadm=1.20.2-00
kubeadm version
````

Now we can plan the upgrade with:

````
sudo kubeadm upgrade plan v1.20.2
````

Let's apply it:

````
sudo kubeadm upgrade apply v1.20.2
````

After upgrading the control-plane components is going to require us to upgrade kubelet and kubectl as well in the node:

````
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubelet=1.20.2-00 kubectl=1.20.2-00
````

After that we can restart kubelet

````
sudo systemctl daemon-reload

sudo systemctl restart kubelet
````

And just uncordon the control plane node <3


### Worker nodes upgrade

Note: In a real-world scenario, you should not perform upgrades on all worker nodes at the same time. Make sure enough nodes are available at any given time to provide uninterrupted service.

But I would do both at the same time.

First let's drain the nodes

````
kubectl drain <worker 1 node name> --ignore-daemonsets --force
````

Then update kubeadm

````
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubeadm=1.20.2-00

kubeadm version
````

Then you can upgrade with kubeadm and upgrade kubelet and kubectl

````
sudo kubeadm upgrade node

sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubelet=1.20.2-00 kubectl=1.20.2-00

sudo systemctl daemon-reload

sudo systemctl restart kubelet
````

The last step is just to uncordon both worker nodes <3
