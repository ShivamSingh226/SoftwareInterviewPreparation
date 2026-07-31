# Kubernetes Cluster

## Worker Node, Master Node, Control Plane and etcd Cluster

- Worker Node: Host Application as container

## Master Nodes

- Master Node: Manage, Plan, Schedule, and Monitor Nodes through **Control Plane**
- etcd cluster: Maintain records in Key-Value format
- kube-scheduler: Type of nodes to be suited appropriate for a container placement
- node-controller: Manging nodes, their onboarding and other aspects
- replication-controller: Desired number of nodes is always available
- controller-manager: Manages both node-controller and replication-controller

- kube-apiserver: Exposes API externally to manage cluster, manages orchestration and communication between different component.

## Worker Nodes
- software that can run container as everything is containerized: **Docker Runtime Engine** or **Container-D**. Installed in every node from master node to worker node.
- kubelet: Communicate with kube-api server and manages the container on the nodes. Kube-api fetches periodically from kubelet regarding the status of the nodes and container on them.

- kube-proxy: Ensures that worker nodes and container on them reaches out to each other and communicate with each other. For example: a service of db exposed to the same pod network and the communication is done between them.

## Docker and Container-D

- To break tightly coupled dependency with Docker, Kubernetes introduced CRI **Container Runtime Interface** as per Open Container Initiatives(OCI) which consists of *imagespec* and *runtimespec* .

- **dockershim** to support docker outside the purview of OCI

- `nerdctl` instead of `docker` like `nerdctl run --name redis:alpine`

- `ctr` command but not widely used as it is obsolete

- `crictl` used to interact with CRI compatible tools, used for debugging, if used to create a container *kubelet* will delete the container created outside the purview of it

## etcd

- Distributed, reliable key-value store

- `kubectl get pods`:kube-apiservice requests status from etcd cluster and reverts back

## Writing YAML file

- `apiVersion`, `kind`, `metadata` and `spec` .


```bash
apiVersion: v1
kind: Pod
metadata:
    name: nginx
    labels:
        app: nginx
        tier: frontend
spec:
    containers: 
     -name: nginx
      image: nginx
```

- `kubectl apply -f pod.yaml` -> pod/nginx created

## Trying out with Labs
**KodeSkool** : Practice Lab for `kubectl` and `nerdctl` commands

## Replication Controller

- Enables more than one pod running in a single cluster 

- **ReplicaSet** requires `selector` in the yaml file.

- It requires `selector`, `matchLabels` and `type`:`frontend` to be equal to selector.


## RollingUpdates

- Scaling the pods one by one ( For example: scaling the pods one by one, disrupting each pods one by one and introducing new and updated one meanwhile)

## Services

- **NodePort Service**: It has a port on the node which forwards request to the specified pod. Makes an internal pod accessible on the port of the node.

- **ClusterIP Service**: An Internal Virtual IP Address inside cluster to facilitate communication between different services

- **Load Balancer**: Distribution of load across different servers

## NodePort

- *Target Port*: 10.244.0.2(Pod)   
*Service Port*: 10.106.1.12(Service)

*Node Port*: 30008 (Exposed on Node)

## ClusterIP
- Virtual IP Address for communication between different nodes

## Load Balancer

- Kubernetes having support to integrate GCP Platform or others to give a load balancer support for four different pods and two different service(if they are in cluster) to route the request to correct service.

## Namespaces

- Kubernetes Cluster - What if everyone deploys in the same cluster?

- Nobody will know who's who?

- So, we will use Namespace to separate it logically from each other

- *Nodes*, *persistentVolumes* and *StorageClasses* are common for cluster

- Two namespaces can have same deployment names

## Kubectl Commands `kubectl explain`

- Describe the configuration of the pods  
`kubectl describe pod pod-name`

- Getting the configuration of the pod  
`kubectl get pods`

- Creating the pod  
`kubectl run <pod-name> --image=<nginx:lates>`

- Creating a YAML file  


```bash
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: demo
spec:
  containers:
    - name: my-container
      image: nginx:latest
      ports:
        - containerPort: 80
```


Then, apply the changes using  
`kubectl apply -f pod.yaml`

Then use `kubectl get pods`

## Kubernetes Deployment

1. kubectl->kube-apiserver->etcd(store values in key-value pair)->kube-controller-manager(Need 3 pods - Check if everything is alright)->kube-scheduler(Choose worker node for hosting the pods) -> kubelet(Present on the worker node to check if all the pods are running or not)

2. *kubelet* reads pod specification, pulls the container image, asks **container runtime env** (Docker or container-d) to create environment.

3. Mounts volumes, configures networking, starts container and reports pod status back to API server


## DaemonSets

- One pod every Node 
- Used for node level agents
- Scales automatically as nodes are added or removed

## Deployments

- Runs a specified number of replicas
- Used for applications like web-servers
- Scales by changing replica count through YAML file of deployment

## Things to learn now:

- ReplicaSets
- Services
- Namespaces
- ConfigMaps
- Secrets
- Ingresses

## What we have in Apps

- Deployment
- ConfigMap
- Secret
- Service
- CronJob
