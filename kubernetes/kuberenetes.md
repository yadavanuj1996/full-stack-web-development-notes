
Kuberenetes (pronounced koo-ber-netes) is container-orchestration system.

1) How kuberenetes (k8s) works:-
There is a lot of VM or Bare metal machines running on the cloud and K8s trasnforms unifies them in API services together that developer can interact with without thinking about the underlying machines (known as nodes in k8s terminology).

2) Core pieces of kubernetes:-

1) Service:- Load balancer that can bring traffic to the pods from external source or from other services inside the cluster.

Services are connected to cloud level load balancers.
K8s request from cloud for ip address and a end user talk to external ip address and that ip address is mapped to cloud level load balancer and that sends traffic to service and that itself is mapped to pods.


2)Deployment:- Under hood use replica sets(Replica sets is used for creating or replicating pods). 
Deployment is represented as a yaml file 

3)PODS -collection of containers colocated on a machine.
 
If we increase our replicaset from 3 to 4 in deployment (i.e., yaml file) kuberenetes self healing nature comes into play and it check that required state needs 4 replicas and there are only 3 running so it will create a new one.

3) Containers:- Container main 3 functions are
1) Taking an application and packaging it so building (sort of binary representation) of your application your software, dependencies , config files so that it runs same on your laptop and same on cloud.

2) Having protocol for distribution around the world easily.
3) Having a isolated environment (playground) for that application to run so that bug in one component does not affect the other component.

4) Liveliness test- The pod is running or not
readiness test - The container is serving or not

A load balancer only start sending traffic to a pod only after it's readiness test
is checked or passed (NOTE: liviliness test should also pass but readiness test determines
whether the load balancer will send traffic or not.).

Rollout and rollbacks 
kuberenetes let our app image update with zero downtime
as the new pod of v2 is created and only after then the
v1 pod will be deleted and load balance will start to move traffic to 
v2 pod,   and after load balancer stops the traffic to got to 
v1 pod still there is a termination frace period which will enabel
to complete the requests that were already made to the particular pod before th
traffic to the v1 pod is cut down by load balancer.
If there is some issue with the new rollout of v2 image of our code we can simply tell the kuberenetes to rollback and it will take our application state back to v1 pods(it keeps the info about the earlier images and deployment inteact with it).


5) How kubernetes Scheduler works:-
When we create a pod, the pod object exists in k8s api but it does not have a node associated with it so it does not have a machine it is scheduled onto and scheduler is continously watching for pods that are in condition (pods that are created but have not been successfully scheduled yet) also scheduler continuously wathcing state of the all the machines(nodes).Scheduler job is to find out in which specific node of various nodes available will the container should run.

Scheduler checks two things 
a) Predicates:- Hard constraints ex:- Memory of node should be 4 GB in a machine. They eliminate the whole machine out of consideration if the required constraints fail.

Mix of system (ex- Memory requirements, node selector) and user constraints.
b) Priorities:- Soft Constraints (It would be nice if every machine in cluster has different amount of workload)
They can be vioalted and give sense of goodness and badness of following a constraint.
ex:- Spreading, Prefer not sick machine


6) Creating Kubernetes build pipelines

  k8s had admissions controller is used when a request comes into cluster the admission controller is used validate the request.

image: myregistry.acr.io/*
above line ensures 

7) Common scenario for usage of kuberenetes
    1) Serving web application 
    2) Let's say if your website have users traffic high in day and low in night and you want to do batch analytics
	you can set the time to run such analytics during night or during low traffic time without affecting much of your
	microservices performance.
    3) To run scheduled jobs ,or run a job that will call another jobs


8) How Volumes and Storage Work in kubernetes
	A volumne is a seperate object defined under the context of kuberenetes pod.
	The volume is associated with pod but is mounted into a container at a particular path.
 
	i) Empry dir :- The directory is present on the machine where pod is located, lifecycle is 
	related to pod life so it can only be used for caching, temporary info like coordination 
	between different containers in application.

  	ii) Persistent Volume:- (cloud mounted volumes) Persistent volume can be mapped to
 	something like azure disk or ISCSI or any persistent volumen types, this kind of disks are not
	dependent on pod life , if pod changes machine the persistent volume will move withpod 
	to new location of pod.

9) The basics of stateful applications in kuberenetes:-

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

10) Secret Mangement in kubernetes:-
	 As pod has multiple container and one of the pod requires a secret like db passowrd or a certificate to access a API or serving a file, there is a built in kuberenetes secret mangament. A Secret resource in kuberenetes is a collection of key-value pairs, and we can multiple key-value pairs within the context of a particular decret, also we can use the key-value pair as contents of file. Ex:-
	dbpassword: foo
	cert: <file> 

We can declare a Secret volume in the list of volumes in Pods and mount the path in particular path we can make the nginx directory check on certs/ folder for the required certificate.

We can also link a Sercret as a ENV variable in kuberneted or a file.	

Kuberenetes stores all the Secrets in a etcd in an Un-Encrypted form , there are various external key mangement store and encrypt the secrets before storing into etcd and even if someone get access to etcd it will contain encrypted key. RBAC ensures that only right people have access to the kubeneted API.It's recommended to store the credentials as kuberenetes secrets and not in docker image, or source control.

10) Kuberenetes and config management
	Config Map is resouce with key value pairs in kubernetes used for config mangement.A Config Map can be
mount as a volume to a pod itself and thus mount it to a container in a particular directory.

Above is useful for configuration that is a file , if configuration is a simple key-value pair we can use a ENV
Variable and easily access it like getenv("Lang")

Rollout of config map is also possible so if with new configuration our app does not work we can do a rollout and go back to prev version of Config Map.

Templating can be used for having base config map and then making basic differences for different environments.

11) Role Based Access Control (RBAC) in kuberenetes:-

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
