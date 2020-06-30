
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

 
