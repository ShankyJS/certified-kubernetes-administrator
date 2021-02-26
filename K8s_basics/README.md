# What is K8s?

" Portable, extensible, open-soure platform for managin containerized workloads and services, that facilitates both declarative configuration and automation. "

## What abbreviation K8s means?

K8s is short for kubernetes, the 8 represents the 8 letters between K and S.

## K8s server structure

If you want to spin up containers you just need to install docker on the machine's and start lifting the containers that you need, but this can be tedious so that's why K8s creates a *layer of abstraction* called "Kubernetes Cluster" that helps to control all the containers within the same cluster.

## K8s main Features

- The primary purpose of K8s is to dynamically manage containers across multiple host systems.
- K8s makes it easier to build reliable, self-healing and scalable applications.
- K8s offers a variety of features to help automate the management of a container app.

# K8S Architectural Overview

## The Control Plane

The control plane is a collection of multiple components responsible for managing the cluster itself globally. Essentially, the control plane controls the cluster.

Individual control plane components can run on any machine in the cluster. But usually are run on dedicated controller machines.

## Control plane components

### kube-api-server

*kube-api-server* serves the *K8s* api, that is the primary interface to the control plane and the cluster itself.

When interacting with your Kubernetes cluster, you will usually do using the Kubernetes API.

### Etcd

Etcd is the backend data store for the Kubernetes Cluster. It provides high-availability storage for all data relating to the state of the cluster.

### kube-scheduler

*kube-scheduler* handles scheduling, the process of selecting an available node in the cluster on which to run containers.

### kube-controller-manager

*kube-controller-manager* runs a collection of multiple controller utilities in a single process. These controllers carry out a variety of automation-related tasks within the Kubernetes Cluster.

### cloud-controller-manager

*cloud-controller-manager* provides an interface between Kubernetes and various cloud platforms. It is only used when using cloud-based resources alongside Kubernetes.

## Nodes

Kubernetes Nodes are the machines where the containers managed by the cluster run. A cluster can have any number of nodes. 

Various node components manage containers on the machine and communicate with the control plane.

## Nodes componenents

## kubelet

*Kubelet* is the Kubernetes agent that runs on each node. It communicates with the control plane and ensures that the containers are up and running as instructed b y the control plane.

Kubelet also handles the process of reporting container status and other data about containers back to the control plane.

## Container runtime

The *container runtime* is not built into Kubernetes. It's separate piece of software that is responsible for actually running containers on the machine.

K8s supports multiple container runtimes, but the most populars are Docker and ContainerD.

## kube-proxy

Is a network proxy that runs on each node and handles tasks related to providing networking between containers and services in the cluster.

## K8s The Big Picture
<img src="https://i.imgur.com/tTRdVsd.png"/>

