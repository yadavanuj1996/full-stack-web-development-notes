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
	


##### pod.yml
```
apiVersion: v1
kind: Pod
metadata:
  name: first-pod
  labels:
    project: qsk-course
spec:
  containers:
    - name: web-ctr
      image: educative1/qsk-course:1.0
      ports:
        - containerPort: 8080

```

#####  svc-cloud.yml
```
apiVersion: v1
kind: Service
metadata:
  name: cloud-lb
spec:
  type: LoadBalancer
  ports:
  - port: 8080
    targetPort: 8080
  selector:
    project: qsk-course




```




# Detailed Notes
Kuberenetes (pronounced koo-ber-netes) is container-orchestration system.

1. How kuberenetes (k8s) works:-
   There is a lot of VM or Bare metal machines running on the cloud and K8s trasnforms unifies them in API services together that developer can interact with without thinking about the underlying machines (known as nodes in k8s terminology).

2. Core pieces of kubernetes:-

i) Service:- Load balancer that can bring traffic to the pods from external source or from other services inside the cluster.

Services are connected to cloud level load balancers.
K8s request from cloud for ip address and a end user talk to external ip address and that ip address is mapped to cloud level load balancer and that sends traffic to service and that itself is mapped to pods.

ii)Deployment:- Under hood use replica sets(Replica sets is used for creating or replicating pods).
Deployment is represented as a yaml file

iii)PODS -collection of containers colocated on a machine.

If we increase our replicaset from 3 to 4 in deployment (i.e., yaml file) kuberenetes self healing nature comes into play and it check that required state needs 4 replicas and there are only 3 running so it will create a new one.

3. Containers:- Container main 3 functions are
1. Taking an application and packaging it so building (sort of binary representation) of your application your software, dependencies , config files so that it runs same on your laptop and same on cloud.

1. Having protocol for distribution around the world easily.
1. Having a isolated environment (playground) for that application to run so that bug in one component does not affect the other component.

1. Liveliness test- The pod is running or not
   readiness test - The container is serving or not

A load balancer only start sending traffic to a pod only after it's readiness test
is checked or passed (NOTE: liviliness test should also pass but readiness test determines
whether the load balancer will send traffic or not.).

Rollout and rollbacks
kuberenetes let our app image update with zero downtime
as the new pod of v2 is created and only after then the
v1 pod will be deleted and load balance will start to move traffic to
v2 pod, and after load balancer stops the traffic to got to
v1 pod still there is a termination frace period which will enabel
to complete the requests that were already made to the particular pod before th
traffic to the v1 pod is cut down by load balancer.
If there is some issue with the new rollout of v2 image of our code we can simply tell the kuberenetes to rollback and it will take our application state back to v1 pods(it keeps the info about the earlier images and deployment inteact with it).

5. How kubernetes Scheduler works:-
   When we create a pod, the pod object exists in k8s api but it does not have a node associated with it so it does not have a machine it is scheduled onto and scheduler is continously watching for pods that are in condition (pods that are created but have not been successfully scheduled yet) also scheduler continuously wathcing state of the all the machines(nodes).Scheduler job is to find out in which specific node of various nodes available will the container should run.

Scheduler checks two things
a) Predicates:- Hard constraints ex:- Memory of node should be 4 GB in a machine. They eliminate the whole machine out of consideration if the required constraints fail.

Mix of system (ex- Memory requirements, node selector) and user constraints.
b) Priorities:- Soft Constraints (It would be nice if every machine in cluster has different amount of workload)
They can be vioalted and give sense of goodness and badness of following a constraint.
ex:- Spreading, Prefer not sick machine

6. Creating Kubernetes build pipelines

k8s had admissions controller is used when a request comes into cluster the admission controller is used validate the request.

image: myregistry.acr.io/\*
above line ensures

7. Common scenario for usage of kuberenetes
   1. Serving web application
   2. Let's say if your website have users traffic high in day and low in night and you want to do batch analytics
      you can set the time to run such analytics during night or during low traffic time without affecting much of your
      microservices performance.
   3. To run scheduled jobs ,or run a job that will call another jobs

8)  How Volumes and Storage Work in kubernetes
    A volumne is a seperate object defined under the context of kuberenetes pod.
    The volume is associated with pod but is mounted into a container at a particular path.

        	i) Empry dir :- The directory is present on the machine where pod is located, lifecycle is
        	related to pod life so it can only be used for caching, temporary info like coordination
        	between different containers in application.

        	ii) Persistent Volume:- (cloud mounted volumes) Persistent volume can be mapped to
        	something like azure disk or ISCSI or any persistent volumen types, this kind of disks are not
        	dependent on pod life , if pod changes machine the persistent volume will move withpod
        	to new location of pod.

9)  The basics of stateful applications in kuberenetes:-

        	It's easier to apply data replication in cloud
        	native application like mongodb and cassandra
        	as compare to the MySql.

        	Replica sets are one way of replication in
        	kuberenetes and each replica set has a RANDOM hash
        	value. Replica sets are not best fit for
        	data replication as if a scaling down a
        	container is choose a random  and deleted while 	many stateful application expect host names to be
        	constant thus making it tough for replica sets
        	to be used with stateful applications.


    Stateful set is similar to replica sets with
    gurantees to make it easier to manage stateful
    application.The stateful sets in kubernetes have
    indices so the replica has stable host names and 	 fixed indexs like 0,1,2and host name are constant
    like my-sever-0, my-sever-1 and so on.  The scaling up and down happens in predictable way. Like if second replica is created it already has a guarantee there is already a replica with index 0 that exists and when we scale down the replica set with highest index will be deleted , if there are 3 container the one with index 2 will be killed first.

    Stateful replica set provide ability to develop DNS names that actually target individual replicas.ex:- "cassandra-0", "cassandra-1"

10. Secret Mangement in kubernetes:-
    As pod has multiple container and one of the pod requires a secret like db passowrd or a certificate to access a API or serving a file, there is a built in kuberenetes secret mangament. A Secret resource in kuberenetes is a collection of key-value pairs, and we can multiple key-value pairs within the context of a particular decret, also we can use the key-value pair as contents of file. Ex:-
    dbpassword: foo
    cert: <file>

We can declare a Secret volume in the list of volumes in Pods and mount the path in particular path we can make the nginx directory check on certs/ folder for the required certificate.

We can also link a Sercret as a ENV variable in kuberneted or a file.

Kuberenetes stores all the Secrets in a etcd in an Un-Encrypted form , there are various external key mangement store and encrypt the secrets before storing into etcd and even if someone get access to etcd it will contain encrypted key. RBAC ensures that only right people have access to the kubeneted API.It's recommended to store the credentials as kuberenetes secrets and not in docker image, or source control.

11. Kuberenetes and config management
    Config Map is resouce with key value pairs in kubernetes used for config mangement.A Config Map can be
    mount as a volume to a pod itself and thus mount it to a container in a particular directory.

Above is useful for configuration that is a file , if configuration is a simple key-value pair we can use a ENV
Variable and easily access it like getenv("Lang")

Rollout of config map is also possible so if with new configuration our app does not work we can do a rollout and go back to prev version of Config Map.

Templating can be used for having base config map and then making basic differences for different environments.

12)Role Based Access Control (RBAC) in kuberenetes:-

    Why do we need it :- We don't want all the memebers of our team to give access to all the resources of our cluster, let's say user1 is given access to resources of user2 then he can delete the work of user1, or if there is some upcoming secret project that one of your team in company is working on you don't want everyone else in company to know about it. Also RBAC makes sure user1 does not know there is any user2 in the with the kubernetes access.

Role are stored as Restful resource in kuberenetes and new roles can also be added it container
verbs:- get,list
nouns:- Pods,Volumes

If a user is granted a role of edit he can get/list/edit (verb) a pod/volume(noun).

Generally a group is given permission for a role let's say a group has been given a role of edit or cluster-admin then anyone who joins the group will have the access provided and anyone who is removed from the group his acess will cease to exist.

Role Binding:-
Role binding is of 2 type:-
i) CLuster Role Binding
ii) Role Binding (Limited to a namespace)

A edit role binded to a namespace can only do the available commands of edit role in that particular namespace. ex:-

/my-team/pods
/your-team/pods

a access of pods of my team will be available to me but not of your team pods.

A cluster Role binding is powerful and gives access to particular role in whole cluster i.e., all of namespace including the ones that will be created in future.

/my-team/role binding ----> edit ---->user 1

a user named user1 is given permission to my-team namespace limiting the scope to my-team namespace and giving level of access of edit Role.

13. Commands:-

a) minikube start (to start the minikube a single node cluster)
b) kubectl cluster-info
Provides cluster details with health check details of the cluster
c) kubectl create -f deployment deployment.yaml
One of the most common Kubernetes object is the deployment object. The deployment object defines the container spec
required, along with the name and labels used by other parts of Kubernetes to discover and connect to the application.

    Creates deployment with the spec given in deployment.yaml file
    deployment.yaml file sample:-

    # This is your deployment.yaml file.
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: webapp1
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: webapp1
      template:
        metadata:
          labels:
            app: webapp1
        spec:
          containers:
          - name: webapp1
            image: katacoda/docker-http-server:latest
            ports:
            - containerPort: 80


d) kubectl get deployment

    As deployment is a object in kuberenetes the above command lists all of the deployed objects.

e) kubectl describe deployment webapp1

    This command will give details of individual deployment (webapp1 in this case).

f) kubectl create -f service.yaml

    The above command creates a service (which is an object in kubernetes) using the spec given in service.yaml file.

    Kubernetes has powerful networking capabilities that control how applications communicate. These networking configurations can also be controlled via YAML.

    All Kubernetes objects are deployed in a consistent way using kubectl.

    service.yaml file sample:-
    # This is your Editor pane.
	apiVersion: v1
	kind: Service
	metadata:
	name: webapp1-svc
	labels:
		app: webapp1
	spec:
	type: NodePort
	ports:
	- port: 80
		nodePort: 30080
	selector:
		app: webapp1

	

g) kubectl get svc
	
	This command will list all the deployed services of our kubernetes cluster.

h) kubectl describe svc webapp1-svc 
	This will get individual detail about the deployed service.

i) kubectl apply -f deployment.yaml

	Scale Deployment ($ are not to be typed with the below commands they are there because of copying
				      from kubectl terminal)

	$ kubectl get deployment
	NAME      READY   UP-TO-DATE   AVAILABLE   AGE
	webapp1   1/1     1            1           24m
	$ kubectl get pods
	NAME                       READY   STATUS    RESTARTS   AGE
	webapp1-6b54fb89d9-zw786   1/1     Running   0          24m

	After increasing the ```replicas``` in deployment.yaml and running the above command
	kubectl apply -f deployment.yaml, the new deployment will be configured and the no of replicas will
	be increased to 4 and kubectl get pods will provide details about 4 pods instead of like previous 1.

	$ kubectl apply -f deployment.yaml
	Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply
	deployment.apps/webapp1 configured
	$ kubectl get deployment
	NAME      READY   UP-TO-DATE   AVAILABLE   AGE
	webapp1   4/4     4            4           25m
	$ kubectl get pods
	NAME                       READY   STATUS    RESTARTS   AGE
	webapp1-6b54fb89d9-qxz8x   1/1     Running   0          23s
	webapp1-6b54fb89d9-wlrzl   1/1     Running   0          23s
	webapp1-6b54fb89d9-xklnn   1/1     Running   0          23s
	webapp1-6b54fb89d9-zw786   1/1     Running   0          26m

	curl host01:30080 command will send the request and will be processed by one of our pods in the current deployment.
					  as 30080 is defined as nodePort in service.yaml the external port will map the request to
					  internal port 80 of the container.


14)  Kubernetes Secret Management

i)	kubectl create -f secret.yaml 	(Creating a secret)

	Use Kubernetes to manage Secrets
	Kubernetes requires secrets to be encoded as Base64 strings.

	(> are not to be typed they are copied during terminal command copying)
	controlplane $ username=$(echo -n "admin" | base64)
	controlplane $ password=$(echo -n "a62fjbd37942dcs" | base64)
	controlplane $ echo "apiVersion: v1
	> kind: Secret
	> metadata:
	>   name: test-secret
	> type: Opaque
	> data:
	>   username: $username
	>   password: $password" >> secret.yaml
	controlplane $ kubectl create -f secret.yaml
	secret/test-secret created

ii) kubectl get secrets		(Listing all the secrets)

	controlplane $ kubectl get secrets
	NAME                  TYPE                                  DATA   AGE
	default-token-m4xkg   kubernetes.io/service-account-token   3      2m4s
	test-secret           Opaque                                2      86s

iii) 	kubectl exec -it secret-env-pod env | grep SECRET_		(NOT RECOMMENDED)			
	(Consuming or using the secrets as env variable)

	In the file secret-env.yaml we've defined a Pod which has environment variables populated
 	from the previously created secret.

	-controlplane $ cat secret-env.yaml
	 	# this is secret-env.yaml file this is the first way to consume a secret in kubernetes
		# using a  env variable (second is consuming a file)
		apiVersion: v1
		kind: Pod
		metadata:
		name: secret-env-pod
		spec:
		containers:
			- name: mycontainer
			image: alpine:latest
			command: ["sleep", "9999"]
			env:
				- name: SECRET_USERNAME
				valueFrom:
					secretKeyRef:
					name: test-secret
					key: username
				- name: SECRET_PASSWORD
				valueFrom:
					secretKeyRef:
					name: test-secret
					key: password
		restartPolicy: Never

	-Launch the Pod using 
		kubectl create -f secret-env.yaml

	-Once the Pod started, you output the populated environment variables.
	 	kubectl exec -it secret-env-pod env | grep SECRET_

	controlplane $ kubectl get pods
	NAME             READY   STATUS    RESTARTS   AGE
	secret-env-pod   1/1     Running   0          17m

iv) Consume a Secret via Volumes (RECOMMENDED APPROACH)

	The use of environment variables for storing secrets in memory can result in them accidentally leaking. The recommend approach is to use mount them as a Volume.

	The Pod specification can be viewed using cat secret-pod.yaml.

	To mount the secrets as volumes we first define a volume with a well-known name, in this case, secret-volume, and provide it with our stored secret.

	volumes:
	- name: secret-volume
	secret:
		secretName: test-secret
	When we define the container we mount our created volume to a particular directory. Applications will read the secrets as files from this path.

	volumeMounts:
	- name: secret-volume
	mountPath: /etc/secret-volume
	Task
	Create our new Pod using kubectl create -f secret-pod.yaml

	Once started you can interact with the mounted secrets. For example, you can list all the secrets available as if they're regular data. For example kubectl exec -it secret-vol-pod ls /etc/secret-volume

	Reading the files allows us to access the decoded secret value. To access username we'd use kubectl exec -it secret-vol-pod cat /etc/secret-volume/username

	For the password, we'd read the password file kubectl exec -it secret-vol-pod cat /etc/secret-volume/password


	The use of environment variables for storing secrets in memory can result in them accidentally leaking. The recommend approach is to use mount them as a Volume.

15) Networking in kubernetes 

	Kubernetes’s advanced networking capabilities allow pods and Services to communicate inside and externally to the cluster’s network. You’ll learn about a variety of Kubernetes services, including Cluster IP, Target Ports, Load Balancer, and more.

	Cluster IP is the default approach when creating a Kubernetes Service. The service is 
	allocated an internal IP that other components can use to access the pods.

	By having a single IP address it enables the service to be load balanced across multiple 
	Pods.
	
	
	
	
	
