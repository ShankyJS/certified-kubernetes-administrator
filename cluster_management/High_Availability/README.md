# High Availability in K8s

K8s facilitates high-availability for applications but this concept can apply as well for the cluster itself to be highly available, to do this you will need multiple control plane nodes.

Control Plane node 1 and 2: Will have kube-api-server -> this connects to a LoadBalanacer to balance the loads to your control plane 1 and 2 clusters. Kubelet of the workers node should connect to that loadbalancer to communicate with the kube-api-server as well.


## Stack Etcd

<img src="https://d33wubrfki0l68.cloudfront.net/d1411cded83856552f37911eb4522d9887ca4e83/b94b2/images/kubeadm/kubeadm-ha-topology-stacked-etcd.svg" height="500px">

This pattern consists on that the ETCD runs in the same nodes of the control-plane nodes. This is for default in kubeadm, this means that the etcd will be created on the control-plane node. 

## External Etcd

<img src="https://d33wubrfki0l68.cloudfront.net/ad49fffce42d5a35ae0d0cc1186b97209d86b99c/5a6ae/images/kubeadm/kubeadm-ha-topology-external-etcd.svg" height="500px">
We can have also multiple external nodes that will run etcd outside of the control-plane nodes.

