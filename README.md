# Learning Kubernetes

## Install kubectl
`` sudo apt-get install -y kubectl ``

## Install docker
`` sudo apt-get install -y docker.io ``

`` sudo systemctl start docker ``

`` sudo systemctl enable docker ``

`` sudo usermod -aG docker $USER ``

## minikube 
is a single node cluster that runs on a virtual machine on your local machine and is used for development and testing purposes.

### Install minikube
`` curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 ``
`` sudo install minikube-linux-amd64 /usr/local/bin/minikube ``

### Start minikube `` minikube start ``

### Stop minikube `` minikube stop ``

# Kubernetes Commands and Concepts
#### Kubernetes consists of a master node and worker nodes where the master node is responsible for managing the cluster and the worker nodes are responsible for running the applications.

#### The master node consists of the following components:
- API Server: It is the entry point for all the REST commands used to interact with the cluster.
- etcd: It is a distributed key-value store used to store the cluster data.
- Scheduler: It is responsible for distributing the workload.
- Controller Manager: It is responsible for regulating the state of the cluster.
- kubelet: It is responsible for communication between the master node and the worker nodes.
- kube-proxy: It is responsible for maintaining the network rules.

#### The worker nodes consist of the following components:
- kubelet: It is responsible for communication between the master node and the worker nodes.
- kube-proxy: It is responsible for maintaining the network rules.
- Container Runtime: It is responsible for running the containers.

### Nodes
- A node can be a physical machine or a virtual machine.
- A node contains the pods that run the applications.
- A node can be created through a command: `` kubectl create node <node-name> ``
- A node can be deleted through a command: `` kubectl delete node <node-name> ``
- A node can be accessed through a command: `` kubectl get node <node-name> ``
- A node can be detailed accessed through a command: `` kubectl describe node <node-name> ``
- A node can be accessed through a service.

### Pods
- A pod is the smallest unit in Kubernetes that can be created, deployed, and managed.
- A pod can contain one or more containers.
- A pod is created through a deployment or a replica set.
- A pod can be created through a command: `` kubectl run nginx --image=nginx ``
- A pod can be deleted through a command: `` kubectl delete pod <pod-name> ``
- A pod can be created or updated through a yaml file: `` kubectl apply -f pod.yaml ``
- A pod can be accessed through a command: `` kubectl get pod <pod-name> ``
- A pod can be detailed accessed through a command: `` kubectl describe pod <pod-name> ``
- A pod can be accessed through a service.

### Jobs
- A job is used to run a task to completion.
- A job can be ran once or multiple times, and it can be parallel or sequential.
- A job can be created or updated through a yaml file: `` kubectl apply -f job.yaml ``
- A job can be deleted through a command: `` kubectl delete job <job-name> ``
- A job can be accessed through a command: `` kubectl get job <job-name> ``
- A job can be detailed through a command: `` kubectl describe job <job-name> ``

### Cron Jobs
- A cron job is used to run a job at a specific time or interval.
- A cron job can be created or updated through a yaml file: `` kubectl apply -f cronjob.yaml ``
- A cron job can be deleted through a command: `` kubectl delete cronjob <cronjob-name> ``
- A cron job can be accessed through a command: `` kubectl get cronjob <cronjob-name> ``
- A cron job can be detailed through a command: `` kubectl describe cronjob <cronjob-name> ``
- A cron job can be paused through a command: `` kubectl patch cronjob <cronjob-name> -p '{"spec": {"suspend": true}}' ``
- A cron job can be resumed through a command: `` kubectl patch cronjob <cronjob-name> -p '{"spec": {"suspend": false}}' ``
- A cron job can be forced through a command: `` kubectl create job --from=cronjob/<cronjob-name> <job-name> ``

### Labels and Selectors
- Labels are key-value pairs that are attached to objects.
- Selectors are used to select objects based on labels.
- You can multi match labels with selectors as based on "AND" or "OR" operators in the selector.
- Labels are used to select objects.
- Labels can be added to an object through a yaml file: `` kubectl apply -f object.yaml ``
- Labels can be added to an object through a command: `` kubectl label object <object-name> <key>=<value> ``
- Labels can be removed from an object through a command: `` kubectl label object <object-name> <key>- ``
- Labels can be showed through a command: `` kubectl get object --show-labels ``
- Labels can be selected through a command: `` kubectl get object -l <key>=<value> `` or `` kubectl get object --selector=<key>=<value> ``

### Annotations
- Annotations are key-value pairs that are attached to objects, its used as informative data.
- Annotations are used to attach metadata to objects.
- Annotations can be added to an object through a yaml file: `` kubectl apply -f object.yaml ``
- Annotations can be added to an object through a command: `` kubectl annotate object <object-name> <key>=<value> ``
- Annotations can be removed from an object through a command: `` kubectl annotate object <object-name> <key>- ``
- Annotations can be showed through a command: `` kubectl get object --show-annotations ``

### Namespaces
- Namespaces are used to organize objects in a cluster.
- When accesss some service through a this convention: `` SERVICE_NAME.NAMESPACE_NAME.svc.cluster.local ``
- Namespaces can be created through a yaml file: `` kubectl apply -f namespace.yaml ``
- Namespaces can be created through a command: `` kubectl create namespace <namespace-name> ``
- Namespaces can be attached to an object through a command with the flag `` --namespace=<namespace-name> `` or `` -n <namespace-name> `` like `` kubectl apply -f object.yaml --namespace=<namespace-name> ``
- Namespaces can be deleted through a command: `` kubectl delete namespace <namespace-name> ``
- Namespaces can be accessed through a command: `` kubectl get namespace <namespace-name> ``
- Namespaces can be detailed through a command: `` kubectl describe namespace <namespace-name> ``
- Namespaces can be accessed through a command: `` kubectl get all --namespace=<namespace-name> `` or `` kubectl get all -n <namespace-name> ``
- Namespaces can be set as default through a command: `` kubectl config set-context --current --namespace=<namespace-name> ``

### Replica Sets
- A replica set is used to create and manage pods.
- A replica set can be created or updated through a yaml file: `` kubectl apply -f replicaset.yaml ``
- A replica set can be deleted through a command: `` kubectl delete replicaset <replicaset-name> ``
- A replica set can be accessed through a service.
- A replica set can be accessed through a command: `` kubectl get replicaset <replicaset-name> ``
- A replica set can be detailed through a command: `` kubectl describe replicaset <replicaset-name> ``
- A replica set can be scaled up or down through a command: `` kubectl scale replicaset <replicaset-name> --replicas=3 ``
- A replica set can be rolled back through a command: `` kubectl rollout undo replicaset <replicaset-name> ``
- A replica set can be rolled out through a command: `` kubectl rollout status replicaset <replicaset-name> ``
- A replica set can get a history through a command: `` kubectl rollout history replicaset <replicaset-name> ``
- A replica set can be paused through a command: `` kubectl rollout pause replicaset <replicaset-name> ``
- A replica set can be resumed through a command: `` kubectl rollout resume replicaset <replicaset-name> ``
- A replica set can be exposed through a service.
- A replica set can be autoscaled through a command: `` kubectl autoscale replicaset <replicaset-name> --min=1 --max=3 --cpu-percent=80 ``
- A replica set can be updated through a command: `` kubectl set image replicaset <replicaset-name> nginx=nginx:1.9.1 ``
- A replica set can be updated through a command: `` kubectl replace -f replicaset.yaml `` 
- A replica set can be updated through a command: `` kubectl edit replicaset <replicaset-name> ``

### Deployments
- A deployment is used to create and manage pods.
- A deployment can be created or updated through a yaml file: `` kubectl apply -f deployment.yaml ``
- A deployment can be deleted through a command: `` kubectl delete deployment <deployment-name> ``
- A deployment can be accessed through a service.
- A deployment can be accessed through a command: `` kubectl get deployment <deployment-name> ``
- A deployment can be detailed through a command: `` kubectl describe deployment <deployment-name> ``
- A deployment can be scaled up or down through a command: `` kubectl scale deployment <deployment-name> --replicas=3 ``
- A deployment can be rolled back through a command: `` kubectl rollout undo deployment <deployment-name> ``
- A deployment can be rolled out through a command: `` kubectl rollout status deployment <deployment-name> ``
- A deployment can get a history through a command: `` kubectl rollout history deployment <deployment-name> ``
- A deployment can be paused through a command: `` kubectl rollout pause deployment <deployment-name> ``
- A deployment can be resumed through a command: `` kubectl rollout resume deployment <deployment-name> ``
- A deployment can be exposed through a service.
- A deployment can be autoscaled through a command: `` kubectl autoscale deployment <deployment-name> --min=1 --max=3 --cpu-percent=80 ``
- A deployment can be updated through a command: `` kubectl set image deployment <deployment-name> nginx=nginx:1.9.1 ``
- A deployment can be updated through a command: `` kubectl replace -f deployment.yaml ``
- A deployment can be updated through a command: `` kubectl edit deployment <deployment-name> ``

## The main difference between a deployment and a replica set is that 
- a deployment is used to manage pods and replica sets, while a replica set is used to manage pods.
- a deployment allows for rolling updates and rollbacks, while a replica set does not.

### Labels and Selectors
- Labels are key-value pairs that are attached to objects.
- Labels are used to select objects.
- Labels can be added to an object through a yaml file: `` kubectl apply -f object.yaml ``
- Labels can be added to an object through a command: `` kubectl label object <object-name> <key>=<value> ``
- Labels can be removed from an object through a command: `` kubectl label object <object-name> <key>- ``
- Labels can be selected through a command: `` kubectl get object --selector=<key>=<value> ``
- Labels can be selected through a command: `` kubectl get object --show-labels ``
- Labels can be selected through a command: `` kubectl get object --selector=<key>=<value> --show-labels ``

### Replication Controllers
- ### Note that a replication controller is deprecated and should be replaced with a replica set because a replica set is more powerful and flexible for managing pods through labels and selectors.
- A replication controller is used to create and manage pods.
- A replication controller can be created or updated through a yaml file: `` kubectl apply -f replicationcontroller.yaml ``
- A replication controller can be deleted through a command: `` kubectl delete replicationcontroller <replicationcontroller-name> ``
- A replication controller can be accessed through a service.
- A replication controller can be scaled up or down through a command: `` kubectl scale replicationcontroller <replicationcontroller-name> --replicas=3 ``

### Networking
#### Kubernetes networking has three network services:
- NodePort: It is used to expose a service on a specific port on each node. // mapping the port of the service to the port of the node like 30001:80
- ClusterIP: It is used to expose a service on a cluster-internal IP.
- LoadBalancer: It is used to expose a service externally using a cloud provider's load balancer.

### Services
- A service is used to expose an application running in a pod.
- A service can be created or updated through a yaml file: `` kubectl apply -f service.yaml ``  
- A service can be created or updated through a command: `` kubectl expose deployment <deployment-name> --type=NodePort --port=80 --target-port=80 ``
- A service can be deleted through a command: `` kubectl delete service <service-name> ``
- A service can be accessed through a node port, a cluster IP, or a load balancer.
- A service can be accessed through a command: `` kubectl get service <service-name> `` or `` kubectl get svc <service-name> ``
- A service can be accessed through a command: `` kubectl describe service <service-name> `` or `` kubectl describe svc <service-name> ``
- A service can be accessed through a command: `` kubectl get endpoints <service-name> `` or `` kubectl get ep <service-name> ``