# Learn Kubernetes: A Deep Dive

### Kubernetes Background
**Kubernetes** is an **application orchestrator**. For the most part, it orchestrates **containerized cloud-native microservices apps**

#### What is an orchestrator
An orchestrator is a system that deploys and manages applications. It can deploy your applications and dynamically respond
to changes. For example, Kubernetes can:
- Deploy your application
- Scale it up and down dynamically according to demand
- Self-heal it when things break
- Perform zero-downtime rolling updates and rollbacks
- And the best part about Kubernetes: it can do all of that without you having to supervise or get involved in decisions. Obviously, you have to set things up in the first place, but, once you’ve done that, you can sit back and let Kubernetes work its magic.

#### What is a containerized app
A containerized application is an app that runs in a container.

Before we had containers, applications ran on physical servers or in virtual machines. Containers are the next iteration
of how we package and run our apps, and they’re faster, more lightweight, and more suited to modern business requirements 
than servers and virtual machines.

Think of it this way:
- Applications ran on physical servers in the age of open-system(roughly in the 1980s and 1990s)
- Applications ran in virtual machines in the age of virtual machines (during the 2000s and into the 2010s)
- Applications run in containers in the cloud-native era (present time)
- While Kubernetes can orchestrate other workload types, including virtual machines and serverless functions, it’s most commonly used to orchestrate containerized apps.

#### What is a cloud-native app
A cloud-native application is an application that is designed to meet modern business demands
(auto-scaling, self-healing, rolling updates, etc.) and can run on Kubernetes.  

Note: They absolutely can run on a public cloud, but they can run anywhere that you have Kubernetes – even your on-premises data center.  

#### What is a microservices app
A microservices app is a business application that is built from lots of small specialized parts that communicate 
and form a meaningful application. 

```
For example, you might have an e-commerce app that comprises all of the following small specialized components:
Web front-end
Catalog service
Shopping cart
Authentication service
Logging service
Persistent store
```
- Each of these individual services can be implemented as a microservice. 
- Typically, each can be coded and looked after by a different team, and each can have its own release cadence and can be scaled independently of all others. 
- For example, you can patch and scale the logging microservice without affecting any of the other application components. 
- Building applications this way is an important aspect of a cloud-native application.

#### Summary
Kubernetes deploys and manages (orchestrates) applications that are packaged and run as containers (containerized) and that 
are built in ways (cloud-native microservices) that allow them to scale, self-heal, and be updated in line with modern business requirements.


### The Operating System of the Cloud
Kubernetes has emerged as the de-facto platform for deploying and managing cloud-native applications. In many ways, 
it’s like an operating system (OS) for the cloud. Consider this:
- You install a traditional OS (Linux or Windows) on a server, and the OS abstracts the physical server’s resources and schedules processes etc.
- You install Kubernetes on a cloud, and it abstracts the cloud’s resources and schedules the various microservices of cloud-native applications.

In the same way that Linux abstracts the hardware differences of different server platforms, Kubernetes abstracts the
differences between different private and public clouds. Net result: as long as you’re running Kubernetes, it doesn’t matter 
if the underlying systems are on-premises in your own data center, edge clusters, or in the public cloud.

With this in mind, Kubernetes enables a true hybrid cloud, allowing you to seamlessly move and balance workloads across multiple 
different public and private cloud infrastructures. You can also migrate to and from different clouds, meaning you can choose a 
cloud today and not have to stick with that decision for the rest of your life.

#### A quick analogy
- Consider the process of sending goods via a courier service. You package the goods in the courier’s standard packaging, put a label on it, and hand it over to the courier the courier abstracts everything else and takes care of scheduling and other logistics.
- It’s the same for apps on Kubernetes. You package the app as a container, give it a declarative manifest, and let Kubernetes take care of deploying it and keeping it running. You also get a rich set of tools and APIs that let you introspect (observe and examine) your app. It’s a beautiful thing.
 


## Kubernetes Principles of Operation
 
### Kubernetes From 40K Feet
At the highest level, Kubernetes is two things:
- A cluster for running applications.
- An orchestrator of cloud-native microservices apps.


**Kubernetes as a cluster**
 - Kubernetes is like any other cluster – a bunch of nodes and a control plane. The control plane exposes an API and 
 records the state in a persistent store; it also has a scheduler for assigning work to nodes. Nodes are where application 
 services run.
 - It can be useful to think of the control plane as the brains of the cluster and the nodes as the muscle. In this analogy, 
 the control plane is the brain because it implements all of the important features, such as auto-scaling and zero-downtime 
 rolling updates. The nodes are the muscle because they do the every-day hard work of executing application code. 
 
**Kubernetes as an orchestrator**
 - Orchestrator is just a fancy word for a system that takes care of deploying and managing applications.



#### How it works
- To make this happen, you start out with an app; you package it up and give it to the cluster (Kubernetes). The cluster is made up of one or more masters and a bunch of nodes.
- The masters, sometimes called heads or head nodes, are in charge of the cluster. This means they make scheduling decisions, perform monitoring, implement changes, respond to events, and more. For these reasons, we often refer to the masters as the control plane.
- The nodes are where application services run, and we sometimes call them the data plane. Each node has a reporting line back to the masters and constantly watches for new work assignments.

![Screenshot 2022-04-16 at 4 01 08 PM](https://user-images.githubusercontent.com/22169012/163671604-eac58ccf-572a-4019-9f2b-278ccee95d8d.png)


To run applications on a Kubernetes cluster, we follow this simple pattern:
- Write the application as small independent microservices in our favorite languages.
- Package each microservice in its own container.
- Wrap each container in its own Pod.
- Deploy Pods to the cluster via higher-level controllers, such as, Deployments, DaemonSets, StatefulSets, CronJobs etc.
  - Deployments offer scalability and rolling updates.   
  - DaemonSets run one instance of a service on every node in the cluster.  
  - StatefulSets are for stateful application components.  
  - CronJobs are for short-lived tasks that need to run at set times.


Kubernetes likes to manage applications **declaratively**. This is a pattern where you describe how you want your application to 
look and feel in a set of YAML files. You POST these files to Kubernetes, then sit back while Kubernetes makes it all happen.

But it doesn’t stop there. Because the declarative pattern tells Kubernetes how an application should look, Kubernetes can watch it and make sure things don’t stray from what you asked for. If something isn’t as it should be, Kubernetes tries to fix it.

### Control Plane (Master)
A Kubernetes cluster is made of masters and nodes. These are Linux hosts that can be virtual machines (VM), bare metal
servers in your data center, or instances in a private or public cloud. A Kubernetes master is a collection of system 
services that make up the control plane of the cluster.

- The simplest setups run all the master services on a single host. However, this is only suitable for labs and test environments. 
- For production environments, multi-master high availability (HA) is a must have. This is why the major cloud providers implement HA masters as part of their hosted Kubernetes platforms, such as Azure Kubernetes Service (AKS), AWS Elastic Kubernetes Service (EKS), and Google Kubernetes Engine (GKE).
- Generally speaking, running 3 or 5 replicated masters in an HA configuration is recommended.
- It’s also considered a good practice not to run user applications on masters. This allows masters to concentrate entirely on managing the cluster.

![Screenshot 2022-04-16 at 7 01 55 PM](https://user-images.githubusercontent.com/22169012/163676866-018e80c1-37cf-4fe7-b3e4-9a895a6797e5.png)


##### The API server
The API server is the Grand Central Station of Kubernetes. All communication, between all components, must go through the API server,  it’s important to understand that internal system components, as well as external user components, all communicate via the same API.
- It exposes a RESTful API that you POST YAML configuration files to over HTTPS. These YAML files, which we sometimes call manifests, contain the desired state of your application. This desired state includes things like; which container image to use, which ports to expose, and how many Pod replicas to run.
- All requests to the API Server are subject to authentication and authorization checks, but, once these are done, the config in the YAML file is validated, persisted to the cluster store, and deployed to the cluster.


##### Cluster store
- The cluster store is the only stateful part of the control plane, and it persistently stores the entire configuration and state of the cluster. As such, it’s a vital component of the cluster – no cluster store, no cluster.
- The cluster store is currently based on etcd, a popular distributed database. As it’s the single source of truth for the cluster, you should run between 3-5 etcd replicas for high availability, and you should provide adequate ways to recover when things go wrong.
- On the topic of availability, etcd prefers consistency over availability. This means that it will not tolerate a split-brain situation and will halt updates to the cluster in order to maintain consistency. However, if etcd becomes unavailable, applications running on the cluster should continue to work, you just won’t be able to update anything.
- As with all distributed databases, the consistency of writes to the database is vital. For example, multiple writes to the same value originating from different nodes needs to be handled. etcd uses the popular RAFT consensus algorithm to accomplish this.


##### The controller manager
- The controller manager implements all of the background control loops that monitor the cluster and respond to events.
- It’s a controller of controllers, meaning it spawns all of the independent control loops and monitors them.
- Some of the control loops include the node controller, the endpoint controller, and the ReplicaSet controller. Each one runs as a background watch loop that is constantly watching the API server for changes – the aim of the game is to ensure the current state of the cluster matches the desired state (more on this shortly).

```
The logic implemented by each control loop is effectively this:
1. Obtain desired state
2. Observe current state
3. Determine differences
4. Reconcile differences
```

This logic is at the heart of Kubernetes and declarative design patterns. Each control loop is also extremely specialized and only interested in its own little corner of the Kubernetes cluster. No attempt is made to over complicate things by implementing awareness of other parts of the system - each control loop takes care of its own business and leaves everything else alone. This is key to the distributed design of Kubernetes and adheres to the Unix philosophy of building complex systems from small specialized parts.

##### The scheduler
- At a high level, the scheduler watches the API server for new work tasks and assigns them to the appropriate healthy nodes. Behind the scenes, it implements complex logic that filters out nodes incapable of running the task and then ranks the nodes that are capable. The ranking system is complex, but the node with the highest ranking score is selected to run the task.

- When identifying nodes that are capable of running a task, the scheduler performs various predicate checks. These include: Is the node tainted? Are there any affinity or anti-affinity rules? Is the required network port available on the node? Does the node have sufficient free resources? Any node incapable of running the task is ignored, and the remaining nodes are ranked according to things such as: Does the node already have the required image? How much free resource does the node have? How many tasks is the node already running? Each criterion is worth points, and the node with the most points is selected to run the task.

- If the scheduler cannot find a suitable node, the task cannot be scheduled and is marked as pending. The scheduler isn’t responsible for running tasks, just picking the nodes a task will run on.


##### The cloud controller manager
If you’re running your cluster on a supported public cloud platform, such as AWS, Azure, GCP, DO, IBM Cloud, etc., your control plane will be running a cloud controller manager. Its job is to manage integrations with underlying cloud technologies and services, such as instances, load balancers, and storage. For example, if your application asks for an internet facing load balancer, the cloud controller manager is involved in provisioning an appropriate load balancer on your cloud platform.


### Nodes
```
Nodes are the workers of a Kubernetes cluster. At a high level, they do three things:

1. Watch the API Server for new work assignments.
2. Execute new work assignments.
3. Report back to the control plane (via the API server).
```

![Screenshot 2022-04-16 at 6 31 13 PM](https://user-images.githubusercontent.com/22169012/163675953-4b41f1d9-65d5-43a8-b2fa-08157058596b.png)


#### Kubelet
- The kubelet is the star of the show on every node. It’s the main Kubernetes agent, and it runs on every node in the cluster. In fact, it’s common to use the terms node and kubelet interchangeably.

- When you join a new node to a cluster, the process installs the kubelet onto the node. The kubelet is then responsible for registering the node with the cluster. Registration effectively pools the node’s CPU, memory, and storage into the wider cluster pool.

- One of the main jobs of the kubelet is to watch the API server for new work assignments. Any time it sees one, it executes the task and maintains a reporting channel back to the control plane.

- If a kubelet can’t run a particular task, it reports back to the master and lets the control plane decide what actions to take. For example, if a kubelet cannot execute a task, it is not responsible for finding another node to run it on. It simply reports back to the control plane, and the control plane decides what to do.

#### Container runtime
- The kubelet needs a container runtime to perform container-related tasks – things like pulling images and starting and stopping containers.

- In the early days, Kubernetes had native support for a few container runtimes, such as Docker. More recently, it has moved to a plugin model called the Container Runtime Interface (CRI). At a high level, the CRI masks the internal machinery of Kubernetes and exposes a clean documented interface for third-party container runtimes to plug into.

- There are many container runtimes available for Kubernetes. One popular example is cri-containerd. This is a community-based, open-source project, porting the CNCF containerd runtime to the CRI interface. It has a lot of support and is replacing Docker as the most popular container runtime used in Kubernetes.

Note: containerd (pronounced “container-dee”) is the container supervisor and runtime logic stripped out from the Docker Engine. It was donated to the CNCF by Docker, Inc. and has a lot of community support. Other CRI-compliant container runtimes exist as well.

#### Kube-proxy 
The last piece of the node puzzle is the kube-proxy. This runs on every node in the cluster and is responsible for local cluster networking. For example, it makes sure each node gets its own unique IP address and implements local IPTABLES or IPVS rules to handle routing and load-balancing of traffic on the Pod network.


### Kubernetes DNS
- As well as the various control plane and node components, every Kubernetes cluster has an internal DNS service that is vital to operations.

- The cluster’s DNS service has a static IP address that is hard-coded into every Pod on the cluster, meaning all containers and Pods know how to find it. Every new service is automatically registered with the cluster’s DNS so that all components in the cluster can find every Service by name. Some other components that are registered with the cluster DNS are StatefulSets and the individual Pods that a StatefulSet manages.
 
![Screenshot 2022-04-16 at 7 12 23 PM](https://user-images.githubusercontent.com/22169012/163677200-efcb14dc-8718-4b61-9aab-17e6cd8c08bc.png)


### Packaging Apps for Kubernetes

For an application to run on a Kubernetes cluster, it needs to tick a few boxes. These include:
1. Being packaged as a container
2. Being wrapped in a Pod
3. Being deployed via a declarative manifest file

It goes like this: you write an application service in a language of your choice. You build it into a container image
and store it in a registry. At this point, the application service is containerized.  

Next, you define a Kubernetes Pod to run the containerized application. Pod is just a wrapper that allows a container to
run on a Kubernetes cluster. Once you’ve defined the Pod, you’re ready to deploy it on the cluster.

#### Deployments
- It is possible to run a stand-alone Pod on a Kubernetes cluster, but the preferred model is to deploy all Pods via higher-level controllers. The most common controller is the Deployment. It offers scalability, self-healing, and rolling updates. You define Deployments in YAML manifest files that specify things like which image to use and how many replicas to deploy.

- Once everything is defined in the Deployment YAML file, you POST it to the API server as the desired state of the application and let Kubernetes implement it.


### The Declarative Model and the Desired State

The declarative model and the concept of desired state are at the very heart of Kubernetes.

In Kubernetes, the declarative model works like this:
1. Declare the desired state of an application (microservice) in a manifest file
2. POST it to the API server
3. Kubernetes stores it in the cluster store as the application’s desired state
4. Kubernetes implements the desired state on the cluster
5. Kubernetes implements watch loops to make sure the current state of the application doesn’t vary from the desired state


- Manifest files are written in simple YAML, and they tell Kubernetes how you want an application to look. This is called the desired state. It includes things such as; which image to use, how many replicas to run, which network ports to listen on, and how to perform updates.

- Once you’ve created the manifest, you POST it to the API server. The most common way of doing this is with the kubectl command-line utility. This sends the manifest to the control plane as an HTTP POST, usually on port 443.

- Once the request is authenticated and authorized, Kubernetes inspects the manifest, identifies which controller to send it to (e.g., the Deployments controller), and records the config in the cluster store as part of the cluster’s overall desired state. Once this is done, the work gets scheduled on the cluster. This includes the hard work of pulling images, starting containers, building networks, and starting the application’s processes.

- Finally, Kubernetes utilizes background reconciliation loops that constantly monitor the state of the cluster. If the current state of the cluster varies from the desired state, Kubernetes will perform whatever tasks are necessary to reconcile the issue.


#### Declarative model vs. imperative model
- It’s important to understand that what we’ve described is the opposite of the traditional imperative model. The imperative model is where you issue long lists of platform-specific commands to build things.
- Not only is the declarative model a lot simpler than long scripts with lots of imperative commands, it also enables self-healing, scaling, and lends itself to version control and self-documentation. It does this by telling the cluster how things should look. If they stop looking like this, the cluster notices the discrepancy and does all of the hard work to reconcile the situation.
- The declarative story doesn’t end there – things go wrong, and things change. When they do, the current state of the cluster no longer matches the desired state. As soon as this happens, Kubernetes kicks into action and attempts to bring the two back into harmony.


