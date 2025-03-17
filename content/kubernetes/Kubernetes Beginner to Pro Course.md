---
title: Kubernetes - Beginner to Pro Course
draft: false
tags: 
    - kubernetes
--- 
Kubernetes: Beginner to Pro course by [DevOps Directive](https://courses.devopsdirective.com/)

🔗 [Link](https://courses.devopsdirective.com/kubernetes-beginner-to-pro/lessons/00-introduction/01-main)

🔗 [Video](https://www.youtube.com/watch?v=2T86xAtR6Fo&t=1s)

## General Notes
- Discovered a new tool called [devbox](https://www.jetify.com/devbox) that allows you to create portable and isolated dev environments locally (instead of something that runs in the cloud like [Gitpod](https://gitpod.io/))

## Technology Overview

**Cluster** - The set of resources that make up the kubernetes systems (made up of nodes)

**Node** - A computer/server. Multiple nodes are joined together to create a cluster.

**Control Plane** - Subset of nodes that perform system tasks (control & manage Kubernetes deployment)

**Data Plane** - Nodes that carry out user workloads (databases, api endpoints, etc.)

## Kubernetes System Components
Multiple smaller parts make the overall Kubernetes platform:
- etcd - key-value store used for storing all cluster data. Serves as the source of truth for the cluster state and configuration
- kube-apiserver - frontend for Kubernetes control plane
- kube-scheduler - Schedules pods onto appropriate nodes based on availability
- kube-controller-manager - runs controller processes. Each controller is a separate process that manages routine tasks (e.g. maintaining desired state of resources, managing replication, handling node operations, etc.)
- cloud-controller-manager - integrates with underlying cloud provider. Handles things like load balances, storage and networking
- kubelet - Agent on each worker node. Manages container lifecycle within pods
- kube-proxy - Network proxy on each node. Maintains network rules to allow communication to and from pods
![Diagram showing Kubernetes system components](https://courses.devopsdirective.com/_next/image?url=%2Fkubernetes-beginner-to-pro%2F02-02-k8s-architecture.jpg&w=1920&q=75)
### kubectl
`kubectl` is the Kubernetes CLI tool.

Example commands:
- `kubectl explain [RESOURCE_TYPE]` - shows all the fields that need to be specified for a particular resource. This can also be used to see the fields for a subfield of the resource, e.g. `kubectl explain Mamespace.metadata`
- `kubectl get namespaces` - Show all namespaces within a cluster
- `kubectl create namespace NAMESPACE_NAME` - Create a namespace in the cluster
- `kubectl apply -f Namepsace.yaml` - Apply the namespace config specified in the file 'Namespace.yaml' to the cluster
- `kubectl delete namespace NAMESPACE_NAME` - Delete the namespace
- `kubectl delete -f Namespace.yaml` - See above
## Kubernetes Resources

### Namespace
- A mechanism to group resources within a cluster
- They can be used to organise applications by assigning a namespace to them (e.g the service.auth app might be added to a namespace called 'auth')
- There are 4 initial namespaces created by the system: `default, kube-system, kube-node-lease and kube-public
- By default, namespaces do not act as a network/security boundary
- Best practise is to create new namespaces for each application
### Pod
- Smallest smallest deployable unit
- Represents a running process on a cluster and encapsulates an app container, storage resources, a unique network IP, and options that given how the containers(s) should run
- Note - In the real world as a developer, you never create pods manually. Usually interact with higher level resources (e.g. `Deployments` and `Jobs`)
- Can have init containers and sidecar containers
### ReplicaSet
- Allows the replication of pods
- Usually never creating a ReplicaSet directly
- Labels are the link between ReplicaSets and Pods
### Deployments
- Adds the concept of 'rollouts' and 'rollbacks'
- Used for long-running stateless apps
- Deployments are the next level up the chain from ReplicaSets
### Service
- An internal load balancer across replicas
- Uses pod labels to determine which pods to serve
- Service types:
	- ClusterID: Internal to the cluster
	- NodePort: Listens on each node in cluster
	- LoadBalancer: Provisions external load balancer