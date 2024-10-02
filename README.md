# Learning Kubernetes

## Install kubectl

`sudo apt-get install -y kubectl`

## Architecture

- Kubernetes is a container orchestration platform that automates the deployment, scaling, and management of containerized applications.
- Kubernetes consists of a master node and worker nodes where the master node is responsible for managing the cluster and the worker nodes are responsible for running the applications.
- The master node consists of the following components:
  - API Server: It is the entry point for all the REST commands used to interact with the cluster.
  - etcd: It is a distributed key-value store used to store the cluster data.
  - Scheduler: It is responsible for distributing the workload.
  - Controller Manager: It is responsible for regulating the state of the cluster.
  - kubelet: It is responsible for communication between the master node and the worker nodes.
  - kube-proxy: It is responsible for maintaining the network rules.
- The worker nodes consist of the following components:
  - kubelet: It is responsible for communication between the master node and the worker nodes.
  - kube-proxy: It is responsible for maintaining the network rules.
  - Container Runtime: It is responsible for running the containers.
- Kubernetes uses a declarative model where the desired state of the cluster is defined in a yaml file and Kubernetes ensures that the actual state of the cluster matches the desired state.
- Kubernetes uses labels and selectors to select objects in the cluster.
- Kubernetes uses namespaces to organize objects in the cluster.
- Kubernetes uses services to expose applications running in pods.
- Kubernetes uses deployments to create and manage pods.
- Kubernetes uses replica sets to create and manage pods.
- Kubernetes uses jobs to run tasks to completion.
- Kubernetes uses cron jobs to run jobs at a specific time or interval.

![Kubernetes Architecture](https://github.com/islamsamy214/learning-kubernetes/blob/master/kubernetes-arch.png?raw=true)

## Install docker

`sudo apt-get install -y docker.io`

`sudo systemctl start docker`

`sudo systemctl enable docker`

`sudo usermod -aG docker $USER`

## minikube

is a single node cluster that runs on a virtual machine on your local machine and is used for development and testing purposes.

### Install minikube

`curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
`sudo install minikube-linux-amd64 /usr/local/bin/minikube`

### Start minikube `minikube start`

### Stop minikube `minikube stop`

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
- A node can be created through a command: `kubectl create node <node-name>`
- A node can be deleted through a command: `kubectl delete node <node-name>`
- A node can be accessed through a command: `kubectl get node <node-name>`
- A node can be detailed accessed through a command: `kubectl describe node <node-name>`
- A node consumption can be accessed through a command: `kubectl top node <node-name>`
- A node can be accessed through a service.

### Pods

- A pod is the smallest unit in Kubernetes that can be created, deployed, and managed.
- A pod can contain one or more containers.
- A pod is created through a deployment or a replica set.
- A pod can be created through a command: `kubectl run nginx --image=nginx`
- A pod can be deleted through a command: `kubectl delete pod <pod-name>`
- A pod can be created or updated through a yaml file: `kubectl apply -f pod.yaml`
- A pod can be accessed through a command: `kubectl get pod <pod-name>`
- A pod can be detailed accessed through a command: `kubectl describe pod <pod-name>`
- A pod can be accessed through a service.

### Jobs

- A job is used to run a task to completion.
- A job can be ran once or multiple times, and it can be parallel or sequential.
- A job can be created or updated through a yaml file: `kubectl apply -f job.yaml`
- A job can be deleted through a command: `kubectl delete job <job-name>`
- A job can be accessed through a command: `kubectl get job <job-name>`
- A job can be detailed through a command: `kubectl describe job <job-name>`

### Cron Jobs

- A cron job is used to run a job at a specific time or interval.
- A cron job can be created or updated through a yaml file: `kubectl apply -f cronjob.yaml`
- A cron job can be deleted through a command: `kubectl delete cronjob <cronjob-name>`
- A cron job can be accessed through a command: `kubectl get cronjob <cronjob-name>`
- A cron job can be detailed through a command: `kubectl describe cronjob <cronjob-name>`
- A cron job can be paused through a command: `kubectl patch cronjob <cronjob-name> -p '{"spec": {"suspend": true}}'`
- A cron job can be resumed through a command: `kubectl patch cronjob <cronjob-name> -p '{"spec": {"suspend": false}}'`
- A cron job can be forced through a command: `kubectl create job --from=cronjob/<cronjob-name> <job-name>`

### Labels and Selectors

- Labels are key-value pairs that are attached to objects.
- Selectors are used to select objects based on labels.
- You can multi match labels with selectors as based on "AND" or "OR" operators in the selector.
- Labels are used to select objects.
- Labels can be added to an object through a yaml file: `kubectl apply -f object.yaml`
- Labels can be added to an object through a command: `kubectl label object <object-name> <key>=<value>`
- Labels can be removed from an object through a command: `kubectl label object <object-name> <key>-`
- Labels can be showed through a command: `kubectl get object --show-labels`
- Labels can be selected through a command: `kubectl get object -l <key>=<value>` or `kubectl get object --selector=<key>=<value>`

### Annotations

- Annotations are key-value pairs that are attached to objects, its used as informative data.
- Annotations are used to attach metadata to objects.
- Annotations can be added to an object through a yaml file: `kubectl apply -f object.yaml`
- Annotations can be added to an object through a command: `kubectl annotate object <object-name> <key>=<value>`
- Annotations can be removed from an object through a command: `kubectl annotate object <object-name> <key>-`
- Annotations can be showed through a command: `kubectl get object --show-annotations`

### Namespaces

- Namespaces are used to organize objects in a cluster.
- When accesss some service through a this convention: `SERVICE_NAME.NAMESPACE_NAME.svc.cluster.local`
- Namespaces can be created through a yaml file: `kubectl apply -f namespace.yaml`
- Namespaces can be created through a command: `kubectl create namespace <namespace-name>`
- Namespaces can be attached to an object through a command with the flag `--namespace=<namespace-name>` or `-n <namespace-name>` like `kubectl apply -f object.yaml --namespace=<namespace-name>`
- Namespaces can be deleted through a command: `kubectl delete namespace <namespace-name>`
- Namespaces can be accessed through a command: `kubectl get namespace <namespace-name>`
- Namespaces can be detailed through a command: `kubectl describe namespace <namespace-name>`
- Namespaces can be accessed through a command: `kubectl get all --namespace=<namespace-name>` or `kubectl get all -n <namespace-name>`
- Namespaces can be set as default through a command: `kubectl config set-context --current --namespace=<namespace-name>`

### Replica Sets

- A replica set is used to create and manage pods.
- A replica set can be created or updated through a yaml file: `kubectl apply -f replicaset.yaml`
- A replica set can be deleted through a command: `kubectl delete replicaset <replicaset-name>`
- A replica set can be accessed through a service.
- A replica set can be accessed through a command: `kubectl get replicaset <replicaset-name>`
- A replica set can be detailed through a command: `kubectl describe replicaset <replicaset-name>`
- A replica set can be scaled up or down through a command: `kubectl scale replicaset <replicaset-name> --replicas=3`
- A replica set can be rolled back through a command: `kubectl rollout undo replicaset <replicaset-name>`
- A replica set can be rolled out through a command: `kubectl rollout status replicaset <replicaset-name>`
- A replica set can get a history through a command: `kubectl rollout history replicaset <replicaset-name>`
- A replica set can be paused through a command: `kubectl rollout pause replicaset <replicaset-name>`
- A replica set can be resumed through a command: `kubectl rollout resume replicaset <replicaset-name>`
- A replica set can be exposed through a service.
- A replica set can be autoscaled through a command: `kubectl autoscale replicaset <replicaset-name> --min=1 --max=3 --cpu-percent=80`
- A replica set can be updated through a command: `kubectl set image replicaset <replicaset-name> nginx=nginx:1.9.1`
- A replica set can be updated through a command: `kubectl replace -f replicaset.yaml`
- A replica set can be updated through a command: `kubectl edit replicaset <replicaset-name>`

### Deployments

- A deployment is used to create and manage pods.
- A deployment can be created or updated through a yaml file: `kubectl apply -f deployment.yaml`
- A deployment can be deleted through a command: `kubectl delete deployment <deployment-name>`
- A deployment can be accessed through a service.
- A deployment can be accessed through a command: `kubectl get deployment <deployment-name>`
- A deployment can be detailed through a command: `kubectl describe deployment <deployment-name>`
- A deployment can be scaled up or down through a command: `kubectl scale deployment <deployment-name> --replicas=3`
- A deployment can be rolled back through a command: `kubectl rollout undo deployment <deployment-name>`
- A deployment can be rolled out through a command: `kubectl rollout status deployment <deployment-name>`
- A deployment can get a history through a command: `kubectl rollout history deployment <deployment-name>`
- A deployment can be paused through a command: `kubectl rollout pause deployment <deployment-name>`
- A deployment can be resumed through a command: `kubectl rollout resume deployment <deployment-name>`
- A deployment can be exposed through a service.
- A deployment can be autoscaled through a command: `kubectl autoscale deployment <deployment-name> --min=1 --max=3 --cpu-percent=80`
- A deployment can be updated through a command: `kubectl set image deployment <deployment-name> nginx=nginx:1.9.1`
- A deployment can be updated through a command: `kubectl replace -f deployment.yaml`
- A deployment can be updated through a command: `kubectl edit deployment <deployment-name>`

## The main difference between a deployment and a replica set is that

- a deployment is used to manage pods and replica sets, while a replica set is used to manage pods.
- a deployment allows for rolling updates and rollbacks, while a replica set does not.

### Labels and Selectors

- Labels are key-value pairs that are attached to objects.
- Labels are used to select objects.
- Labels can be added to an object through a yaml file: `kubectl apply -f object.yaml`
- Labels can be added to an object through a command: `kubectl label object <object-name> <key>=<value>`
- Labels can be removed from an object through a command: `kubectl label object <object-name> <key>-`
- Labels can be selected through a command: `kubectl get object --selector=<key>=<value>`
- Labels can be selected through a command: `kubectl get object --show-labels`
- Labels can be selected through a command: `kubectl get object --selector=<key>=<value> --show-labels`

### Replication Controllers

- ### Note that a replication controller is deprecated and should be replaced with a replica set because a replica set is more powerful and flexible for managing pods through labels and selectors.
- A replication controller is used to create and manage pods.
- A replication controller can be created or updated through a yaml file: `kubectl apply -f replicationcontroller.yaml`
- A replication controller can be deleted through a command: `kubectl delete replicationcontroller <replicationcontroller-name>`
- A replication controller can be accessed through a service.
- A replication controller can be scaled up or down through a command: `kubectl scale replicationcontroller <replicationcontroller-name> --replicas=3`

### Networking

#### Kubernetes networking has three network services:

- NodePort: It is used to expose a service on a specific port on each node. // mapping the port of the service to the port of the node like 30001:80
- ClusterIP: It is used to expose a service on a cluster-internal IP.
- LoadBalancer: It is used to expose a service externally using a cloud provider's load balancer.

#### Difference between a node port, and a load balancer is that: 
a node port is used to expose a service on a specific port on each node, while a load balancer is used to expose a service externally using a cloud provider's load balancer, so you have to know each node port to access the service, but with the load balancer you can access the service through a single IP address.

### Services

- A service is used to expose an application running in a pod.
- A service can be created or updated through a yaml file: `kubectl apply -f service.yaml`
- A service can be created or updated through a command: `kubectl expose deployment <deployment-name> --type=NodePort --port=80 --target-port=80`
- A service can be deleted through a command: `kubectl delete service <service-name>`
- A service can be accessed through a node port, a cluster IP, or a load balancer.
- A service can be accessed through a command: `kubectl get service <service-name>` or `kubectl get svc <service-name>`
- A service can be accessed through a command: `kubectl describe service <service-name>` or `kubectl describe svc <service-name>`
- A service can be accessed through a command: `kubectl get endpoints <service-name>` or `kubectl get ep <service-name>`

### Ingress
- An ingress is used to expose an application running in a pod to the outside world.
- An ingress can be created or updated through a yaml file: `kubectl apply -f ingress.yaml`
- An ingress can be deleted through a command: `kubectl delete ingress <ingress-name>`
- An ingress can be accessed through a command: `kubectl get ingress <ingress-name>`
- An ingress can be detailed through a command: `kubectl describe ingress <ingress-name>`
- An ingress can be accessed through a command: `kubectl get ingress <ingress-name> -o yaml`
  #### Note: 
    - An ingress controller is used to manage the ingress resources in a cluster, through a controller like Nginx, Traefik, or HAProxy.
    - An ingress rule is used to define the routing rules for the ingress controller, through a rule like a path, a host, or a service.
    - Ingress servicePort: 80 should match the Service's port: 80
    - nodePort: 30080 is used when accessing the service externally via node IPs and is not used by the Ingress, so you can comment it out.

### Environment Variables

- Environment variables can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- Environment variables can be added to a pod through a command: `kubectl set env pod <pod-name> <key>=<value>`
- Environment variables can be removed from a pod through a command: `kubectl set env pod <pod-name> <key>-`
- Environment variables can be accessed through a command: `kubectl exec -it <pod-name> -- env`
- Environment variables can be accessed through a command: `kubectl exec -it <pod-name> -- printenv`
- Environment variables can be accessed through a command: `kubectl exec -it <pod-name> -- env | grep <key>`

### Config Maps

- A config map is used to store configuration data in key-value pairs.
- A config map can be created or updated through a yaml file: `kubectl apply -f configmap.yaml`
- A config map can be created or updated through a command: `kubectl create configmap <configmap-name> --from-literal=<key>=<value>`
- A config map can be created or updated through a command: `kubectl create configmap <configmap-name> --from-file=<path>`
- A config map can be deleted through a command: `kubectl delete configmap <configmap-name>`
- A config map can be accessed through a command: `kubectl get configmap <configmap-name>`
- A config map can be detailed through a command: `kubectl describe configmap <configmap-name>`
- A config map can be generated through a command: `kubectl create configmap <configmap-name> --from-literal=<key>=<value> --dry-run=client -o yaml > configmap.yaml`

### Secrets

- A secret is used to store sensitive data in key-value pairs.
- A secret can be created or updated through a yaml file: `kubectl apply -f secret.yaml`
- A secret can be created or updated through a command: `kubectl create secret generic <secret-name> --from-literal=<key>=<value>` or `kubectl create secret generic <secret-name> --from-file=<path>`
- A secret can be deleted through a command: `kubectl delete secret <secret-name>`
- A secret can be accessed through a command: `kubectl get secret <secret-name>`
- A secret can be detailed through a command: `kubectl describe secret <secret-name>`
- A secret can be generated through a command: `kubectl create secret generic <secret-name> --from-literal=<key>=<value> --dry-run=client -o yaml > secret.yaml`
- A secret can be encoded through a command: `echo -n '<value>' | base64`
- A secret can be decoded through a command: `echo -n '<value>' | base64 --decode`
- A secret can be accessed through a command: `kubectl get secret <secret-name> -o yaml` then `echo -n '<value>' | base64 --decode`

### service account

- A service account is used to authenticate and authorize pods to access the Kubernetes API.
- A service account can be created or updated through a yaml file: `kubectl apply -f serviceaccount.yaml`
- A service account can be created or updated through a command: `kubectl create serviceaccount <serviceaccount-name>`
- A service account can be deleted through a command: `kubectl delete serviceaccount <serviceaccount-name>`
- A service account can be accessed through a command: `kubectl get serviceaccount <serviceaccount-name>`
- A service account can be detailed through a command: `kubectl describe serviceaccount <serviceaccount-name>`
- A service account can be accessed through a command: `kubectl get serviceaccount <serviceaccount-name> -o yaml`

### Requirements and Limits

- Requirements and limits are used to specify the amount of resources that a pod can use.
- Requirements and limits can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- Requirements and limits can be added to a pod through a command: `kubectl set resources pod <pod-name> --requests=<key>=<value> --limits=<key>=<value>`
- Requirements and limits can be removed from a pod through a command: `kubectl set resources pod <pod-name> --requests=<key>- --limits=<key>-`
- Requirements and limits can be accessed through a command: `kubectl describe pod <pod-name>`
- Requirements and limits can be accessed through a command: `kubectl get pod <pod-name> -o yaml`
- Requirements and limits can be accessed through a command: `kubectl top pod <pod-name>`

### Taints

- A taint is used to repel pods from a node.
- A taint can be added to a node through a command: `kubectl taint node <node-name> <key>=<value>:<effect>`
- A taint can be removed from a node through a command: `kubectl taint node <node-name> <key>-`
- A taint can be accessed through a command: `kubectl describe node <node-name>`
- A taint can be accessed through a command: `kubectl get node <node-name> -o yaml`

### Tolerations

- A toleration is used to allow pods to tolerate taints on a node.
- A toleration can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- A toleration can be added to a pod through a command: `kubectl set tolerations pod <pod-name> <key>=<value>:<effect>`
- A toleration can be removed from a pod through a command: `kubectl set tolerations pod <pod-name> <key>-`
- A toleration can be accessed through a command: `kubectl describe pod <pod-name>`
- A toleration can be accessed through a command: `kubectl get pod <pod-name> -o yaml`

### Node Selector

- A node selector is used to select nodes for a pod.
- A node selector can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- A node selector can be added to a pod through a command: `kubectl set node selector pod <pod-name> <key>=<value>`
- A node selector can be removed from a pod through a command: `kubectl set node selector pod <pod-name> <key>-`
- A node selector can be accessed through a command: `kubectl describe pod <pod-name>`
- A node selector can be accessed through a command: `kubectl get pod <pod-name> -o yaml`

### Node Label

- A node label is used to add labels to a node.
- A node label can be added to a node through a command: `kubectl label node <node-name> <key>=<value>`
- A node label can be removed from a node through a command: `kubectl label node <node-name> <key>-`
- A node label can be accessed through a command: `kubectl describe node <node-name>`
- A node label can be accessed through a command: `kubectl get node <node-name> -o yaml`

### Node Affinity

- A node affinity is used to specify the nodes that a pod can be scheduled on.
- A node affinity is the same as a node selector but with more options so it more complicated.
- A node affinity can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- A node affinity can be added to a pod through a command: `kubectl set node affinity pod <pod-name> <key>=<value>`
- A node affinity can be removed from a pod through a command: `kubectl set node affinity pod <pod-name> <key>-`
- A node affinity can be accessed through a command: `kubectl describe pod <pod-name>`

### Difference between a node affinity or selector and a toleration is that

- a node affinity or selector is used to select nodes for a pod, while a toleration is used to allow pods to tolerate taints on a node.
- Example: if we have 5 pods (red, blue, green, other, other) and have 5 nodes(red, blue, green, other, other)
  - if we used the node affinity or selector with the red pod and the red node only, the other pod might be scheduled on the red node.
  - if we used the toleration with the red pod and the red node only, the red pod might be scheduled on the other node.
  - if we used the node affinity or selector and the toleration with the taints, we will make sure that the red pod will be scheduled on the red node, and the other pod will be scheduled on the other node.

### Multi-Container Pods
- A multi-container pod is used to run multiple containers in a single pod that share the same resources.
- A multi-container pod can be created or updated through a yaml file: `kubectl apply -f pod.yaml`
- A multi-container pod can be deleted through a command: `kubectl delete pod <pod-name>`
- A multi-container pod can be accessed through a command: `kubectl get pod <pod-name>`
- A multi-container pod can be detailed through a command: `kubectl describe pod <pod-name>`
- A multi-container pod can be accessed through a command: `kubectl exec -it <pod-name> --container=<container-name> -- command`

### Readiness Probes
- A readiness probe is used to check if a pod is ready to serve traffic.
- A readiness probe can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- A readiness probe can be added to a pod through a command: `kubectl set readiness pod <pod-name> <key>=<value>`
- A readiness probe can be removed from a pod through a command: `kubectl set readiness pod <pod-name> <key>-`
- A readiness probe can be accessed through a command: `kubectl describe pod <pod-name>`
- A readiness probe can be accessed through a command: `kubectl get pod <pod-name> -o yaml`

### Liveness Probes
- A liveness probe is used to check if a pod is alive and restart it if it is not.
- A liveness probe can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- A liveness probe can be added to a pod through a command: `kubectl set liveness pod <pod-name> <key>=<value>`
- A liveness probe can be removed from a pod through a command: `kubectl set liveness pod <pod-name> <key>-`
- A liveness probe can be accessed through a command: `kubectl describe pod <pod-name>`
- A liveness probe can be accessed through a command: `kubectl get pod <pod-name> -o yaml`

### Logging
- Logging is used to monitor the logs of a pod.
- Logging can be accessed through a command: `kubectl logs <pod-name>`  
- Logging can be accessed through a command: `kubectl logs <pod-name> --container=<container-name>` or `kubectl logs <pod-name> -c <container-name>`
- Logging can be accessed through a command: `kubectl logs <pod-name> --follow` or `kubectl logs <pod-name> -f`

### Network Policies
- A network policy is used to control the traffic between pods.
- A network policy can be created or updated through a yaml file: `kubectl apply -f networkpolicy.yaml`
- A network policy can be deleted through a command: `kubectl delete networkpolicy <networkpolicy-name>`
- A network policy can be accessed through a command: `kubectl get networkpolicy <networkpolicy-name>`
- A network policy can be detailed through a command: `kubectl describe networkpolicy <networkpolicy-name>`
- A network policy can be accessed through a command: `kubectl get networkpolicy <networkpolicy-name> -o yaml`
#### Note: Solutions supports network policies such as Kube-router, Calico, Romana, Calico, Cilium, and Weave Net, So you have to install one of them to use network policies, and for the solutions that do not support network policies such as Flannel, you can use the network policies through the network plugin such as CNI.

### Volumes
- A volume is used to store data in a pod.
- A volume can be added to a pod through a yaml file: `kubectl apply -f pod.yaml`
- A volume can be added to a pod through a command: `kubectl set volume pod <pod-name> <key>=<value>`
- A volume can be removed from a pod through a command: `kubectl set volume pod <pod-name> <key>-`
- A volume can be accessed through a command: `kubectl describe pod <pod-name>`
- A volume can be accessed through a command: `kubectl get pod <pod-name> -o yaml`

### Persistent Volumes
- A persistent volume is used to store data in a pod.
- A persistent volume can be created or updated through a yaml file: `kubectl apply -f persistentvolume.yaml`
- A persistent volume can be deleted through a command: `kubectl delete persistentvolume <persistentvolume-name>`
- A persistent volume can be accessed through a command: `kubectl get persistentvolume <persistentvolume-name>`
- A persistent volume can be detailed through a command: `kubectl describe persistentvolume <persistentvolume-name>`
- A persistent volume can be accessed through a command: `kubectl get persistentvolume <persistentvolume-name> -o yaml`

### Persistent Volume Claims
- A persistent volume claim is used to request a persistent volume.
- A persistent volume claim can be created or updated through a yaml file: `kubectl apply -f persistentvolumeclaim.yaml`
- A persistent volume claim can be deleted through a command: `kubectl delete persistentvolumeclaim <persistentvolumeclaim-name>`
- A persistent volume claim can be accessed through a command: `kubectl get persistentvolumeclaim <persistentvolumeclaim-name>`
- A persistent volume claim can be detailed through a command: `kubectl describe persistentvolumeclaim <persistentvolumeclaim-name>`
- A persistent volume claim can be accessed through a command: `kubectl get persistentvolumeclaim <persistentvolumeclaim-name> -o yaml`

### Storage Classes
- A storage class is used to define the type of storage that a persistent volume uses.
- A storage class can be created or updated through a yaml file: `kubectl apply -f storageclass.yaml`
- A storage class can be deleted through a command: `kubectl delete storageclass <storageclass-name>`
- A storage class can be accessed through a command: `kubectl get storageclass <storageclass-name>`
- A storage class can be detailed through a command: `kubectl describe storageclass <storageclass-name>`
- A storage class can be accessed through a command: `kubectl get storageclass <storageclass-name> -o yaml`

### Stateful Sets
- A stateful set is used to manage stateful applications, that require stable and unique network identifiers, persistent storage, and ordered deployment, so when you delete a pod, it will be recreated with the same name.
- A stateful set can be created or updated through a yaml file: `kubectl apply -f statefulset.yaml`
- A stateful set can be deleted through a command: `kubectl delete statefulset <statefulset-name>`
- A stateful set can be accessed through a command: `kubectl get statefulset <statefulset-name>`
- A stateful set can be detailed through a command: `kubectl describe statefulset <statefulset-name>`
- A stateful set can be accessed through a command: `kubectl get statefulset <statefulset-name> -o yaml`

### Headless Services
- A headless service is used to access the pods directly without a load balancer.
- This is usually used with a stateful set to access the pods directly, to get the unique network identifiers, just to make sure that you are accessing the right pod.
- A headless service can be created or updated through a yaml file: `kubectl apply -f service.yaml`
- A headless service can be deleted through a command: `kubectl delete service <service-name>`
- A headless service can be accessed through a command: `kubectl get service <service-name>`
- A headless service can be detailed through a command: `kubectl describe service <service-name>`
- A headless service can be accessed through a command: `kubectl get service <service-name> -o yaml`
