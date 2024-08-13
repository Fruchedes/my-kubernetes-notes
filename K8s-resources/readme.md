
## Resource Types

🚨 **Note:** You should follow this ordering (and this is the order they are covered in the video course)

- **Namespace**: Provides a way to divide cluster resources between multiple users.
- **Pod**: The smallest and simplest Kubernetes object. Represents a set of running containers on your cluster.
- **ReplicaSet**: Ensures that a specified number of pod replicas are running at any given time.
- **Deployment**: Manages stateless applications, providing features such as rolling updates and rollbacks.
- **Service**: Defines a logical set of pods and a policy by which to access them.
- **Job**: Creates one or more pods that run to completion.
- **CronJob**: Schedules jobs to run at specified times or intervals.
- **DaemonSet**: Ensures that a copy of a pod runs on all (or some) nodes in the cluster.
- **StatefulSet**: Manages stateful applications, providing guarantees about the ordering and uniqueness of pods.
- **ConfigMap**: Store configuration data that can be consumed by pods.
- **Secret**: Manages sensitive information, such as passwords, OAuth tokens, and ssh keys.
- **Ingress**: Manages external access to the services in a cluster, typically HTTP.
- **GatewayAPI**: Manages traffic routing within the cluster, providing advanced routing capabilities.
- **PersistentVolume and PersistentVolumeClaim**: Manages persistent storage for pods.
- **RBAC (Role-Based Access Control)**: Manages permissions within the cluster.

### Out of Scope Resource Types

- **LimitRange**: Specifies resource constraints for resources within a namespace.
- **NetworkPolicy**: Controls the network traffic flow at the IP address or port level within the Kubernetes cluster.
- **MutatingWebhookConfiguration**: Defines webhooks that can mutate incoming requests to the Kubernetes API server.
- **ValidatingWebhookConfiguration**: Defines webhooks that can validate incoming requests to the Kubernetes API server.
- **HorizontalPodAutoscaler**: Automatically scales the number of pods in a deployment or replica set based on observed CPU utilization or other custom metrics.
- **CustomResourceDefinition**: Allows users to define their own resource types and make the Kubernetes API server handle them (covered in a later section!).


#### Why do companies adopt kubernetes?
- **Container Orchestration**: simplifies the management, deployment, scaling of your containerized applications
- **Service Discovery, autoscaling and Load Balancing**; where applications can be automatically discovered by other services, scaled up or down based on demand, and distributed
- **Simplifies deployments**supports different deployments strategies, Rolling Update & Rollbacks,  release new versions of applications and to revert to previous versions if needed
- **Storage Orchestration, Self-Healing, Secrets and Configuration Management** inbuilt mechanism for healing, managing storage and securing sensitive information
- **Multi-Cloud and Hybrid Cloud Support** supports deployment across omprem and multicloud environments
- **Role-Based Access Control (RBAC)**
- **Pods and Multi-Container SupportMonitoring and Logging** intergrates various monitoring tools to perform health checks
- **Highly available and has self healing capabilities**: scale up and down based on workloads and helps your application beacome resilient. I f a container fails it is restarted over and over


#### MONOLITHIC ARCHITECTURE: is are monolithic stacks
>> design approach where application stacks that are developed, tightly coupled and deployed as a single unit or codebase. What does that mean? All components are part of a single application Frontend, logic and backend.
>>The Applications share the same memory space
- **Examples of monolith stacks**
>LAMP: Linux, web server, Mysql
>MEAN: nosql, expressjs, Angular, Nodejs
>JEE: Java, Spring, Tomcat/Jboss/Wblogic, Mysql
>Django Stack: Python, Django, PostgreSQL
- **Benefits**: 
>Easy for small teams to develop and test 
>Doesn't require complex networking  and has a lower overhead
>Has only only a few points of entry 

- **Cons**
>Require the whole application to be deployed
>Doesn't scale well if parts of the application breaks
>Diffcult to update all application dependecies and libraries

#### MICROSERVICE ARCHITECTURE; 
is a design approach where different parts of an application stack are developed seperately, decoupled, deployed as a microservices,  operates independently. Applications communicate with each other using well-defined APIs and services and each microservice 

 **Benefits**
>can deploy without impacting other services 
>Easie to update software versions of dependencies
>Increased fault tolerance


#### KUBERNETES
 is an open-source container orchestration platform designed for automating the deployment, scaling, and management of containerized applications. 

- **Alternatives to KUBERNETES**: Apache Mesos, Openshift, Nomad, Juju, Tanzu, IBM, AKS, EKS, GCP, Suse rancher, 
- **Cluster orchestration**: gcloud, ekctl, kubectl, aksctl
- **Container platform**: Podmad, docker

- **Pod**: smallest deployable unit in kubernetes, represents a collection of one or more containers running in your cluster
- **Node**: smallest fundamental unit of computing hadware, represent single machines in cluster
and status of a node staust contains adderss, condition, capacity and info
- **Containers**: Light weight isolated environments that comprises an application and it dependencies
- **Container runtime**: software responsible for managing and running containers on a host system
- **Container orchestration**: process of managing containers in a distributed environment
- **Cluster**: group of nodes that work together to run containerized apps and manages the underlying infrastructure
- **Heapster**: performance monitoring and metrics collection system for data collected by kublet.
- **Master nodes**: manages, plans, schedules, monitors all activities within the cluster, communicates with worker nodes to ensure all applications in the cluster are running smoothly.
- **comprised of**
- **Etcd**: Keyvalue database that stores cluster information mostly in Json, Yaml format.
- **Scheduler**: Assigns pods to new Nodes based on resource availability.
- **Controller manager**: Ensures the desired state of the cluster by making sure a specific number of pods are running. Runs various controllers like the :
     - **Node controller**: monitors and manages the health of nodes, 
     - **Replication controller**: ensures specific number of pods are running at all times
     - **Namespace controller**: creates and manages namespaces in cluster
     - **Job controller**: Manages batch or on-time jobs that run to completion
     - **Deployment controller**: manges deployment and scaling of applications
     - **Endpoint controller**: manages endpints withservices
- **Api-server**: gateway/entry-point in to the Kubernetes cluster, processes, handles API request from users, applications  and  other components to interact with the cluster. authenticates, authorizes and validates request handling CRUD create read update and delete operations.

- **Worker nodes**: runs the containers and executes the workloads-
comprised of 
- *Kubelet**; Agent, monitors and manages the pods state, replaces failed pods
- **Containerd engine**: runtime environment for our container, responsible 4 creating and managing containers
- **Kubeproxy**: Manages communication between Pods and the external world. Maintains network rules for load balancing and routing.

#### KUBERNETES STABDARD INTERFACE
- **Container interface:** used to execute and run container processes within the kube system. examples containerd, cri-o
- **Container network interface:** defines how container network is setup and defined in the kubernetes ecosystem such calico, Flannel, cilium, AWSVPC plugin, Azure CNI, GPC CNU
- **Container storage interfaces:** standard interface to provide durable persistent storage to containers. Examples EBS CSI-driver, Secrets store CSI-driver, Azure Disk SCI-driver

- **Kubeconfig**: stored in ~/.kube/config contains information about cluster, user credentials, certfificates and context
- **Service files**: contains information about networking such as clusterIP, NodePort, Loadbalancer, Selectors
- **Deployment files**: defines the desired state of deployment, pod replicas, container images and resource limits
- **Config maps**- stores application config files in plain format
kubectl create configmap myconfigmao --from literal=env=dev
- **Use cases: create env variables**
- **Secrets**: stores sensitive data like Password, API keys, in an encrypted format
echno -n 'name you want to encode' | base64
echo -n 'admin' ./username.txt
echno -n 'snap' ./ password.txt
kubectl create secret generic mysecret --from=file=./username.txt --from=./password.txt

- **Deployment**: manages lifecycle of apllications including deployment, scaling, rollingout(gradually updaing the application), rollback reverting back to a preious version)
- **Replica set**: ensures a specific number of pods are running  and it's used for scaling
- **Daemon set**: objects that are ran on every node in a cluster  and are used for logging, monitoring .
- **Stateful set**: objects that manages stateful applications requiring persistent storage, network identities such as database, message queries

- **Headless service**:  manage network access to a set of Pods without using the standard load-balancing features.  a headless service provides DNS records that map to the individual Pods.
 Enables direct communication between Pods, such as with StatefulSets
- **Sidecar**:  specialized containers that run to completion before the main application containers in a Pod start.
- **Init container**:
>Useful: when we want to perform data migration or pre-processing tasks before the application starts.
>Labels: used to identify and group resources
>>>**Selectors**: are used to query and select resources based on their labels
>>**Equity based selector**: select resources based on certain criteria that are equitable or balanced. 
>>**Equality based selector**:  feature for selecting resources based on exact label values or simple logical conditions.
Node selectors:
>>**Service account**: used grant access permission  to pods and apps in your cluster enabling apps to interract with th API server
usecases: grant specific permissions, run applications with different roles

#### 4 resources under RBAC role based acess control authorization mechanism
- **Cluster binding**: granting persmission and access right with in cluster
- **Role binding**: granting permission and access right with in namespace
- **Roles**: set of rules that define permissions and access rights to specificed resources within namespace
- **Cluster role**: used to grant permission to users to manage resources inthe cluster 
- **Service**: provides stable identity and endpoint that other apps can use to intereact
- **Liveness probe**: checks the health of the container and restarts the container
- **Readiness probe**: determines when to start accepting traffic
>>**Startup probe**:

### DEPLOYMENT TYPES: 
- **Rollbacks**: reverting to previous stable state after an update has introduced issues or failures
- **Rolling updates**; default deployment replaces old pods with new ones ensuring a number of pods are available and healthty at all times
- **Blue-green deployment**: traffic is redirected from the prod to new green env and can be switched back
- **Canary deployment**: allows you to test a subset 

- **VOLUMES**: used to provide persistent staorage for containers
- **ReadWriteOnce (RWO)** – The volume is mounted with read-write access for a single Node in your cluster. Any of the Pods running on that Node can read and write the volume’s contents.
- **ReadOnlyMany (ROX)** – The volume can be concurrently mounted to any of the Nodes in your cluster, with read-only access for any Pod.
- **ReadWriteMany (RWX)** – Similar to ReadOnlyMany, but with read-write access.
- **ReadWriteOncePod (RWOP)** – This new variant, introduced as a beta feature in Kubernetes v1.27, enforces that read-write access is provided to a single Pod. No other Pods in the cluster will be able to use the volume simultaneously.
### TYPES OF VOLUMES: 
- **local** – Data is stored on devices mounted locally to your cluster’s Nodes.
- **hostPath** – Stores data within a named directory on a Node (this is designed for testing purposes and doesn’t work with multi-Node clusters).
- **nfs** – Used to access Network File System (NFS) mounts.
- **iscsi**– iSCSI (SCSI over IP) storage attachments.
- **csi** – Allows integration with storage providers that support the Container Storage Interface (CSI) specification, such as the block storage services provided by cloud platforms.
- **cephfs** – Allow the use of CephFS volumes.
- **fc** – Fibre Channel (FC) storage attachments.
- **rbd** – Rados Block Device (RBD) volumes.
- **PV**  are cluster wide storage resources/objects that allow pods to access storage from defined device
- **PVC**. request for storage resources  used to mount persistent volume into a Pod. such as Elasticblock, Azure Disk, Vsphere volume and CSI driver
- **Network policies**: define rules that specify how pods communicates and other endpoints
- **Ingress**: manages external access to services provides LB, HTTP routes, SSL terminations
- **ingress rules**: defines how traffic is allowed into selected pods
- **Egress rules**: deifnes how traffic is allowed to flow out of the selected pods

- **TLS** referes to transport Layer security 
- **NGINX INGRESS CONTROLLER** managing and routing incoming HTTP and HTTPS traffic to services within the cluster. NGINX Ingress Controller uses NGINX as the underlying reverse proxy and load balancer, providing features like host-based routing, path-based routing, TLS termination,
- **EGRESS** controlled and filtered to restrict access to external resources or enforce security policies.
- **SET MANAGER**: assigns certificates to applications
- **VERTICAL POD AUTOSCALER**: adjusts the CPU and memory resource requests of pods based on their resource usage patterns. VPA helps optimize resource allocation by dynamically scaling the resource requests of pods to match their actual resource utilization. 
- **HORIZONTAL POD AUTOSCALER**: number of pod replicas based on observed CPU or custom metrics. HPA helps scale applications horizontally by increasing or decreasing the number of pod replicas in response to changes in resource utilization
HPA

#### SERVICES IN KUBERNETES
- **SERVICES**: abstraction that defines a logical set of pods and policy by which to access them.
- **ClusterIP**: Exposes the service within the cluster, makes it reachable only within cluster
- **NodeIP**: Exposes the service through a static port on each node
- **Loadbalancer**: Exposes the service using  a loadbalancer to evenly distrbute traffic
- **External name**: Services will be mapped to a DNS name.
- **HEADLESS SERVICE**:  enables you to reach ports without accessing via proxy.

#### NETWORKING IN KUBERNETES
- **Networking**: CNI stands for container network interface, manages the way pods and containers connect to the network. Different flavours of CNI's such as Calico, Flannel, Weavenet, Antrea, Tigera Seucure, Mellanox VDPA, kube router
- **Calico**: open-source
- **Flannel**: CNI plugin that uses layer 3 networking
- **Weave**: CNI plugin that provides scalable, networking policies 
- **Cilium**: best CNI plugin, provides best security, observability and good for complex clusters
- **Kube-router**: lightweight CNI plugin Loadbalancer with loadbalancing features and network policiess

#### WHY use CALICO? Provides ###
- **Advanced networking policies**: define fine-frained networking policies  and rules over containers based on labels, ports
- **Scalability**: Handles large clusters with ease 
- **Cross-Cluster networking**: has the capacity to connect multiple clusters together
- **Border Gateway Protocol routing**: supports BGP routing good for onprem
- **Security**: encrypts network traffic so only authoriszed pods can communicate with respective pods

#### VOLUMES KUBERNETES
- **Ephemeral** means if containers are restarted they would loose their data and it requires persistance
- **EmptyDir**: used to share volumes between multiple containers within a pods
                  Data is stored in volumes that reside inside the Pods only

- **hostPath**: helps access data of the pods or container volumes from the host machine
                Replicates data of the volumes on the host machine, if changes on the host are made, it is refelcted on the pods volumes

- **Persistent volume**: process of storing data in the Cloud such as EBS, Azure disk
To get a Persistent volume, you need to claim the volume via the help of of a Persistent Volume Claim

## Liveness Probe in KUBERNETES
- **LivenessProbe**: used to check the health of your application by specifying that in the manifest file.
A 0 output of livenessProbe means the application is running perfectly
LivenessProbe repeats the process  after seconds or minutes
Liveness Probe also recreates pods when it detects the application health checks are unevenly yoked

**ConfigMaps and Secrets in KUBERNETES**
- **ConfigMap: used to store configuration data which is non-confidential in key-value pairs by decoupling the application to get rid of the hard-corded values

- **Secrets**: stores sensitive info such as password, API keys, TLS certificate. 
Provides extra layer of security encodes and decodes using base64-encoded format
Can be mounted in volumes in pods
is a feature that encrypts data stores sensitve data up to 1MB 


#### KUBERNETES JOBS
Jobs are used to run workloads, log rotation, batch processes, backup scripts. 
**Key features of the Jobs**:
● One-time Execution: If you have a task that needs to be executed one time whether
it’s succeed or fail then the job will be finished.
● Parallelism: If you want to run multiple pods at the same time.
● Scheduling: If you want to schedule a specific number of pods after a specific time.
● Restart Policy: You can specify whether the Job should restart if fails


#### SECURITY IN KUBERNETES
Apply security updates 
Restrict access to ETCD
implement network segmentation and define policy rukes
implement vulnerability scanning
Define resource quota and limits
use images from authorized repos only

**KUBERNETES POD LIFECYCLE**
There are multiple types of states for the Pod lifecycle that we will discuss here:

1. Pending: When a pod is created it has to go through the pending status in which Master nodes allocate the nodes to where to create the pod. The pods will remain in the pending state until all the necessary resources are allocated such as CPU, memory, and storage.
2. Running: Once the pod has been scheduled to a node, it comes into the Running Status. Once the pod comes into a running state, the containers within the pods will be creating and doing the tasks that have been provided in the manifest file.
3. Succeeded: Once the pods have completed their task then, the pods come in the succeeded state and then terminates.
4. Failed: Once the pods intend to create but due to some issues the pods are not creating and showing the Failed state leads to issues with the configurations which need to be addressed by the creator of the file.
5. CrashLoopBackOff: This is the advanced state of a Failed state where the container is crashing and restarts. To fix this issue, the creator of the file needs to check the manifest file.
6. Unknown: In some cases, the Kubernetes may lose the connection with the nodes to
create the pods that show the unknown status of the particular pod.
7. Termination: When a pod is no longer available it comes in the termination process.
Once the pod is deleted, it can not restart again the same pods and is removed from the
entire Kubernetes cluster.

There are some conditions that come under while creating Pods:

● Initialized: This condition shows whether all the init containers have started successfully
or not. If the status is false it means the init containers have not started.
● Ready: This condition shows the pod is ready to use.
● ContainersReady: As the name suggests, if the containers are ready within a pod it will
show True in the status.
● PodScheduled: This condition shows that the pod has been scheduled on the node.


**KUBERNETES REQUEST QUOTAS**

**ResourceQuota**: helps manage and distribute resources accoirding to the requirements

● **Limit**: Limit specifies that the container, pod, or namespace will have the limit resources where if the objects will exceed the limit then, the object won’t create.

● **Request**: The request specifies that the container, pod, or namespace needs a particular amount of resources such as CPU and memory. But if the request is greater than the limit then, Kubernetes won’t allow   the creation of pods or containers.

Now, there are some conditions or principles for requests and limit which needs to be
understood.
Let’s understand with hands-on and theoretical.
1. If the requests and limits are given in the manifest file, it works accordingly.
2. If the requests are given but the limit is not provided then, the default limit will be used.
3. If the request

- **Service Account**: A service account provides an identity for processes that run in a Pod. This is how Kubernetes authorizes API requests.
- **RBAC (Role-Based Access Control)**: RBAC is a method of regulating access to computer or network resources based on roles assigned to individual users within an enterprise.
- **Cluster Role**: Cluster-wide roles define permissions on cluster-scoped resources.
- **Role**: Roles define permissions within a namespace. Not tied to namespaces
- **Role Binding**: Role bindings bind roles to subjects. A subject can be a user, group, or service account. permission with in cluster
- **DaemonSet**: A DaemonSet ensures that all (or some) nodes run a copy of a Pod.
- **StatefulSet**: A StatefulSet manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.
Label: Labels are key/value pairs that are attached to objects like Pods, Services, and Deployments to organize and select subsets of objects.
- **Namespaces**: Namespaces provide a way to divide cluster resources between multiple users or teams.
- **Cluster**: A cluster consists of at least one worker node and at least one master node.
- **Pods**: Pods are the smallest and simplest Kubernetes objects. A Pod represents a single instance of a running process in your cluster.
- **Deployment**: A Deployment provides declarative updates for Pods and ReplicaSets.

- **ReplicaSet**: A ReplicaSet ensures that a specified number of pod replicas are running at any given time and works on eaulity controller-only. 
- **Replication Controller**: ensures a specified number of pods are running

Replicaset and replication are both repsonsible for vailability and autoscaling of pods, both ensures specified number of pods are running. 

- **Labels**: defined in keyvalue-pairs, similar to tags, used to organise k8s objects suchs as pods, nodes
- **Equality based selectors**: select/filter objects by label key and values
- **Set-based selectors**: select objects with a particular key with specified values

## Kubernetes webhook authentification:
 is an HTTPS service that recieved a request in defined format
manages webhook authentification via valid certficate, static token file, openID connect tokens and service accounts
Process: user generates a token to call for the Kube Api
The token is receieved by the kubernetes api passes through an auth webhook in predefined format
Webhook validates token and returns status in predefined format


Kubernetes validation webhook:

Autoscaler:
daemon set: replicates pods across your nodes in the cluster, used for running node monitoring, collecting logs from nodes, backing up node data
stateful set: ensures pods are created in a specific order
replication controller :
replicaset:


kubectl get role -A
kubectl get --all-namespaces
~/.ssh
~/.kube/config





create a server volume

hcloud server create --image ubuntu-20.04 --name kelson-ubuntu --type cpx21 --location  ash --user-data-from-file user_data.sh --volume kelson-vol1


How to get the cpu of a pod
kubectl get pod podame-o=jsonpath='{.spec.containers[0].resources.requests.cpu}'

Mastering Kubernetes
------------------------------------------------------------
Master nodes: manages the clusters
manages, plans, schedules and monitors nodes
------------------------------------------
Worker nodes: Host applications
------------------------------------------
Master nodes components
------------------------------------------
-ETCD: database that stores cluster information on nodes, configs, secrets, accounts, roles, bindings, roles, Pods in the keyvalue format.
-distrubuted reliable keyvalue store that is simple and fast
-Keyvalue database that stores information in any format mostly Json, Yaml
Access etcd using
./etcdctl (list all the commands that it supports)
./etcdctl set key1 value1
./etcd get key1
what version is etcd= ./etcdctl --version
to change the the etcd version from version 2 to 3
sets version 2 to 3
etcdclt_API3 ./etcdctl version
export etcdctl_API=3  ./etcdctlversion
sets a value
./etcdctl set key1 value1
gets a value
./etcdctl get key1
set up cluster using kubeadmin
Kube admin deploys the etcd as a pod in the kube system name space
kubectl get pods -n kube-system
kubectl get serviceaccount -n kube-system
kubectl get clusterrolebinding
---------------------------------------------
API Server:
-Authentificates users, validates request, retrieves data , updates data
-Acts as the gateway to the Kubernetes cluster.
-Accepts commands and communicates with other components.
Kube admin deploys the API-server as a pod in the kube system name space
To access the API-server
kubectl get pods -n kube-system
located on th master node as
cat etc/kubernetes/manifests/kube-apiserver.yaml
cat /etc/systemd/system/kube-apiserver.service
ps -aux | grep kube-api-server
---------------------------------------------------------
Controller Manager:
-Ensures the desired state of the cluster.
-Monitors, manages and controls various controllers, which manage different aspects of the system.responsible for availability and scalability
-Node controller: monitors and checks the status of the nodes. Checks the status every 5 seconds and waits for 40 seconds to mark the nodes unreachable and gives it 5 minutes to come back 
-Replication controller: makes sure the desired number of pods are running at all times in a replication group
Kube admin deploys the API-server as a pod in the kube system name space
kubectl get pods -n kube-system
located on the master note at
cat etc/kubernetes/manifests/kube-controller-manager.yaml
cat /etc/systemd/system/kube-controller-manager.service
ps -aux | grep kube-controller-manager
-------------------------------------------------------------------
Scheduler:
Assigns  (containers) to individual pods to  Nodes based on resource availability. 
Distributes workload evenly across the cluster.
Node (Minion/Worker Node):
Kube admin deploys the Scheduler as a pod in the kube system name space on the master node
kubectl get pods -n kube-system
# located on the master note at
cat etc/kubernetes/manifests/kube-scheduler.yaml
cat /etc/systemd/system/kube-scheduler.service
ps -aux | grep kube-scheduler
-------------------------------------------------------------
Worker Nodes components
------------------------------------------------------------------------
