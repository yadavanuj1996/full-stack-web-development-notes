# Quick Start Kubernetes
	
### What is kubernetes 
	Kuberenetes is an open-source container-orchestration system for automating computer application deployment, scaling and management. 
	At its core , Kubernetes is and orchestrator of cloud-native microservices applications.
		
	Cloud Native application must:- 
	1. Scale on demand
	    Scaling on demand is the ability for an application and associated infrastructure to automatically scale up and down based on demand.
      	    If configured correctly, Kubernetes can automatically scale your applications and infrastructure up when demand increases and scale 
	    them down when the demand drops off.


	2. Self-heal applications
		But for now, when you deploy an application on Kubernetes, you will have to specify what the application should look like. 
		The following specifications will be necessary:
			-The number of instances of each microservice
			-The names of the networks to attach to
		Kubernetes saves this as your desired state and monitors your application to make sure it always matches this desired state.
		If something changes, for example if an instance crashes, Kubernetes notices this and spins up a replacement. This is called self-healing.
	
	3. Zero-downtime rolling updates
		Zero-downtime rolling updates is just a fancy way of saying you can incrementally update parts of an application without
		having to shut it down and without clients even noticing. You will see this in action later in the course.
	
	4. Run anywhere
		One final point of interest regarding cloud-native is that a cloud-native application is not an application that
		only runs in the public cloud. No! A cloud-native application can run anywhere you have Kubernetes, such as AWS, Azure,
		Linode, your on-premises datacenter, or even your Raspberry Pi cluster at home.
	
	To summarize, cloud-native applications can self-heal, automatically scale, and be updated without downtime. 
	They can also run wherever you have Kubernetes.

### Why Do We Need Kubernetes?

 Kubernetes also does an amazing job of abstracting underlying cloud and server infrastructure. This basically allowed Kubernetize to commoditize infrastructure.

 #### OS of the cloud

 - Why tech companies need Kubernetes#
 “Abstracting and commoditizing infrastructure” is a fancy way of saying that Kubernetes makes it so you don’t have to worry which cloud or servers your applications are running on. In fact, this is at the heart of the idea that Kubernetes is the operating system (OS) of the cloud. So, in the same way, Linux and Windows mean you do not have to care if your applications are running on Dell, Cisco, HPE, or Nigel Poulton servers. Using Kubernetes means that you do not have to care if your applications are running on AWS or Azure.

 - Why the user community needs Kubernetes#
 It has already been stated that Kubernetes can abstract lower-level on-prem and cloud infrastructure, allowing you to write your applications 
 to run on  ubernetes without even knowing which cloud is behind it. Well, this has a few side benefits, including:

 You can deploy to one cloud today and switch to another tomorrow.
 You can run multi-cloud
 You can ramp onto a cloud and then ramp off back to on-prem more easily.

### What Does kubernetes Look Like?

#### Master and Nodes


##### OS of the cloud

Kubernetes has already been established as the OS of the cloud. As such, it sits between the applications and infrastructure. 
Kubernetes runs on infrastructure, and applications run on Kubernetes.
	
![Screenshot 2021-11-13 at 11 50 04 AM](https://user-images.githubusercontent.com/22169012/141608421-0cabaea3-b26b-4898-a99d-ccb3b511f48c.png)
	
The illustration shows four Kubernetes installations running on four different infrastructure platforms. Because Kubernetes
abstracts the underlying infrastructure, the application at the top of the diagram can run on any of the Kubernetes installations.
You can also migrate it from one Kubernetes installation to another.

- A Kubernetes installation is known as a Kubernetes cluster.
- There are a couple of things worth clarifying here:
It is unusual for a single Kubernetes cluster to span multiple infrastructures.
For example, you likely won’t see Kubernetes clusters that span multiple clouds. Likewise, you’ll rarely see clusters that 
span on-prem and the public cloud. This is mainly due to network speed and reliability. Generally speaking, you want high-speed 
reliable networks connecting the Nodes in a cluster.

- Although Kubernetes can run on many platforms, applications that run on Kubernetes have stricter requirements. You will learn about this 
later on in the chapter, but Windows applications will only run on Kubernetes clusters with Windows Nodes, Linux applications only
run on clusters with Linux Nodes, and applications written for ARM/Raspberry Pis require clusters with ARM Nodes.
	
- A Kubernetes cluster consists of one or more machines that have Kubernetes installed on them. The machines can be physical servers,
virtual machines (VM), cloud instances, your laptop, Raspberry Pis, and more. Installing Kubernetes on these machines and
connecting them together creates a Kubernetes cluster. After creating a cluster, you can deploy applications to that cluster.

- Machines in a Kubernetes cluster are, normally, referred to as Nodes.

- Speaking of Nodes, a Kubernetes cluster contains two types of Nodes:
	- Master Nodes
	- Worker Nodes
	- Usually, Master Nodes are referred to as “Masters” and Worker Nodes are called “Nodes”.

Masters host the control plane and Nodes are where you run user applications.

It is good practice for the Masters to exclusively run control plane services (no user applications). 
All user applications should run on Nodes.


#### Masters
	
Masters host the control plane. That is a fancy way of referring to the brains of the cluster.

With this in mind, it is good practice to have more than one Master in order to maintain high availability (HA). This way,
if one of them fails, the cluster can remain operational. It is common to have 3 or 5 Masters in a production cluster
and to spread them across failure domains. It is not wise to stick them all in the same room, under the same leaky air
conditioning unit, functioning on the same glitchy electricity supply.

1. Assuming you have to create a highly available control plane with 3 Masters. Each one should be in a separate failure domain with
different network infrastructures and distinct power infrastructures, etc.

2. Masters run the following services that form the control plane:
	- API Server
	- Scheduler
	- Store
	- Cloud controller

##### API server
The API Server is the only part of a Kubernetes cluster that you directly interact with. When you send commands to the cluster,
they go to the API server. When you receive responses, they come from the API server.

##### Scheduler
The Scheduler chooses which Nodes to run the user applications on.

##### Store
The Store is where the state of the cluster and all the applications are stored.

##### Cloud controller
The Cloud controller allows Kubernetes to integrate with cloud services, such as storage and load-balancers. The hands-on examples 
that will come up in later chapters will help you integrate a cloud load-balancer with an application that you will deploy to a Kubernetes cluster.



#### Nodes

##### What is Node?
- A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the control plane. A Node can have multiple pods, and the Kubernetes control plane automatically handles scheduling the pods across the Nodes in the cluster. 
- Every Kubernetes Node runs at least:
	- Kubelet, a process responsible for communication between the Kubernetes control plane and the Node; it manages the Pods and the containers running on a machine.
	- A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.

Nodes run user applications and can either be Linux or Windows Nodes. Linux Nodes run Linux applications, whereas Windows Nodes run 
Windows applications.

All Nodes run two main services, namely:
- Kubelet
- Container runtime



##### Kubelet
The kubelet is the main Kubernetes agent. It joins the Node to the cluster and communicates with the control plane, in charge of 
notifying when tasks are received and reporting on the status of those tasks.

##### Container runtime
The container runtime starts and stops containers.

Note: In the past, Kubernetes would use docker as its container runtime. However, Kubernetes 1.20 announced that support for the 
Docker container runtime would be dropped in a future release of Kubernetes. Although Kubernetes will stop supporting Docker as a runtime, 
it will continue to support images created by Docker.


#### Hosted Kubernetes
Hosted Kubernetes is where your cloud provider rents you a Kubernetes cluster. Sometimes, it is called Kubernetes as a Service.

In the hosted model, the cloud provider builds the Kubernetes cluster, owns the control plane, and is responsible for all of the following:

- Control plane performance
- Control plane availability
- Control plane updates


You, the user, are responsible for:
- Worker Nodes
- User applications
- Paying the bill

![Screenshot 2021-11-13 at 12 45 02 PM](https://user-images.githubusercontent.com/22169012/141609790-3d1a2cbb-07cb-420a-83a4-8a21c8b71da8.png)



Although Kubernetes orchestrates and runs containers, these containers must be wrapped in a Kubernetes construct called a Pod.
### What is a Pod?
- A Pod is a lightweight wrapper found around a container. In fact, the terms container and Pod are, sometimes, used interchangeably. For now, you need to know that Kubernetes runs containers inside of Pods – in the same way that VMware runs applications inside of VMs, Kubernetes runs containerized applications inside of Pods.


## Kubernetes Commands

#### Commands
kubectl is a command-line utility used to communicate with kubernetes cluster
- kubectl get nodes
- kubectl apply -f pod.yml (To create a pod from pod.yml file)
- kubectl get pods
- kubectl port-forward --address 0.0.0.0 first-pod 8080:8080 (kubectl port-forward TYPE/NAME [options] LOCAL_PORT:REMOTE_PORT)
- kubectl describe pod first-pod
- kubectl get services (To list all services)
- kubectl describe svc <service-name> (To get details about a service)
- kubectl port-forward --address 0.0.0.0 service/cloud-lb 8080:8080.  (For port forwarding a service running in kubernetes in local system)
- kubectl delete svc cloud-lb (To delete a service)
- kubectl delete pod first-pod (To delete a pod)
- kubectl config view

```
kubectl get - list resources. 
kubectl describe - show detailed information about a resource. 
kubectl logs - print the logs from a container in a pod. 
kubectl exec - execute a command on a container in a pod. 
```


##### Pod Deployment
	
**pod.yml**
	
```
apiVersion: v1
kind: Pod
metadata:
  name: diy-pod
  labels:
    project: task-DIY
spec:
  containers:
  - name: test-container-server
    image: educative1/qsk-course:1.0
    ports:
    - containerPort: 8080

```
- **apiVersion** and **kind** is basically telling Kubernetes to deploy a Pod based on version 1 (v1) of the Pod specification.
- **metadata**: The metadata block lists the Pod name and a single label
	- **name**: helps us identify and manage the Pod when it is running
	- **label**: (project = qsk-course) is useful for organizing Pods and associating them with other objects, such as load balancers. 
- **containerPort**: containerPort defines the port on which app can be reached out inside the container.
	
	
##### Service Deployment
	
**svc-cloud.yml**
	
```
apiVersion: v1
kind: Service
metadata:
  name: diy-test-cloud-lb
  labels:
    app: test-svc-server
spec:
  type: LoadBalancer
  ports:
  - port: 8080
    targetPort: 8080
  selector:
    project: qsk-course
```

**Metadata Name and App Labels**
- **name** in **metadata** is the name of service, when you fire **kubectl get services** you will get the service name (i.e., diy-test-cloud-lb)
- The **app** label passed in **labels** in **metadata** is used in deployment to use a given service for linking it to pods, so that pods will get network access.
- **type** in **spec** represents type of service. Options:
	- ClusterIP
	- NodePort
	- LoadBalancer
- ports
	- **port**: Port exposes the Kubernetes service on the specified port within the cluster. Other pods within the cluster can communicate with this server on the specified port.
	- **targetPort**: TargetPort is the port on which the service will send requests to, that your pod will be listening on. Your application in the container will need to be listening on this port also (in pod using containerPod).
 
 **Other points**
- Kubernetes uses a dedicated Service object to provide network connectivity to applications running in Pods
- The metadata section names the Service “cloud-lb”.
- The spec section is where the magic happens. The spec.type: LoadBalancer field tells Kubernetes to provision an internet-facing load balancer on the underlying cloud platform.
- For example, if your cluster runs on AWS, this Service will automatically provision an AWS Network Load Balancer (NLB) or Classic Load Balancer (CLB). This spec section will configure an internet-facing load-balancer on the underlying cloud that will accept traffic on port 8080 and forward on port 8080 to any Pods with the project: qsk-course label.
	

## Kubernetes Deployments
- Kubernetes has another dedicated object called a Deployment to provide self-healing. In fact, Deployments also enable scaling and rolling updates.
- As with Pods and Service objects, Deployments are defined in YAML manifest files.

There are two important elements to the working of a Deployment.
- The Deployment object
	- The Deployment object is the YAML configuration that defines an application. It states things like which container to run, what network port to listen on, and how many instances (Pods) to deploy.
- The Deployment controller
	- The Deployment controller is a control plane process, which is constantly monitoring the cluster to ensure that all the Deployment objects are running as they are supposed to.

#### Deployment Yaml File
	
**deployment.yml**
	
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: qsk-deploy
spec:
  replicas: 5
  selector:
    matchLabels:
      project: qsk-course
  template:
    metadata:
      labels:
        project: qsk-course
    spec: 
      containers:
      - name: qsk-pod
        imagePullPolicy: Always
        ports:
        - containerPort: 8080
        image: edxxxxive1/qsk-course:1.0
	
```
- **kind**: Type of oject being defined (Pod, Service, Deployment)
- **matchLabels**: Tells the Deployment controller to match labels
- **project** in matchLabels -> selector represents which Pods to manage
- **name** in metadata represents the name of deployment
	- If you trigger kubectl get deployments command you will get this name (i.e., qsk-deploy)
- **replicas** in spec represents how pod replicas is required
- **containerPort** represents the Network Port
- **image** is your Docker Image

	
This nesting, or wrapping, is important in understanding how everything works.
- The container provides the OS and other application dependencies.
- The Pod provides metadata and other constructs for the container to run on Kubernetes.
- The Deployment provides cloud-native features, including self-healing.

![Screenshot 2022-04-14 at 9 53 42 AM](https://user-images.githubusercontent.com/22169012/163313284-9d251c3e-1f57-4457-b3c6-0e741588291a.png)
```	
NOTE: Deployments wrap a Pod spec, which in turn wraps a container, which in turn
      houses an application and its dependencies.
```

	
### Miscellaneous Points
	
#### Namespaces
- Namespaces are Kubernetes objects which partition a single Kubernetes cluster into multiple virtual clusters. Each Kubernetes namespace provides the scope for Kubernetes Names it contains; which means that using the combination of an object name and a Namespace, each object gets an unique identity across the cluster.
- In Kubernetes, namespaces provides a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc).

#### What is a NodePort?
- A NodePort is an open port on every node of your cluster. Kubernetes transparently routes incoming traffic on the NodePort to your service, even if your application is running on a different node.

#### Service Types
- **ClusterIP**: Exposes the service on a cluster-internal IP. Choosing this value makes the service only reachable from within the cluster. This is the default ServiceType

- **NodePort**: Exposes the service on each Node’s IP at a static port (the NodePort). A ClusterIP service, to which the NodePort service will route, is automatically created. You’ll be able to contact the NodePort service, from outside the cluster, by requesting **\<NodeIP\>:\<NodePort\>**.
	
	- kubectl describe service minikube-test-service will display NodePort
	- kubectl describe node minikube-multinode-demo-m02 will show InternalIP i.e., NodeIP

- **LoadBalancer**: Exposes the service externally using a cloud provider’s load balancer. NodePort and ClusterIP services, to which the external load balancer will route, are automatically created.

	
### To Check if pod is linked to a service 
- The best way is follow labels and selectros
- Your pod have a label section, and the service use it in the selector section
- You can find the selectors of your service with:
	- kubectl describe svc cass-operator-service
- You can  list your labels with:
	- kubectl get pods --show-labels
