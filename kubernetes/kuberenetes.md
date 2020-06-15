
Kuberenetes (pronounced koo-ber-netes) is container-orchestration system.

How kuberenetes (k8s) works:-
There is a lot of VM or Bare metal machines running on the cloud and K8s trasnforms unifies them in API services together that developer can interact with without thinking about the underlying machines.

Core pieces of kubernetes:-

1) Service:- Load balancer that can bring traffic to the pods from external source or from other services inside the cluster.

Services are connected to cloud level load balancers.
K8s request from cloud for ip address and a end user talk to external ip address and that ip address is mapped to cloud level load balancer and that sends traffic to service and that itself is mapped to pods.


2)Deployment:- Under hood use replica sets(Replica sets is used for creating or replicating pods). 
Deployment is represented as a yaml file 

3)PODS -collection of containers colocated on a machine.
 
If we increase our replicaset from 3 to 4 in deployment (i.e., yaml file) kuberenetes self healing nature comes into play and it check that required state needs 4 replicas and there are only 3 running so it will create a new one.

Containers:- Container main 3 functions are
1) Taking an application and packaging it so building (sort of binary representation) of your application your software, dependencies , config files so that it runs same on your laptop and same on cloud.

2) Having protocol for distribution around the world easily.
3) Having a isolated environment (playground) for that application to run so that bug in one component does not affect the other component.

Liveliness test- The pod is running or not
readiness test - The container is serving or not

A load balancer only start sending traffic to a pod only after it's readiness test
is checked or passed (NOTE: liviliness test should also pass but readiness test determines
whether the load balancer will send traffic or not.).

kuberenetes let our app image update with zero downtime
as the new pod of v2 is created and only after then the
v1 pod will be deleted and load balance will start to move traffic to 
v2 pod,   and after load balancer stops the traffic to got to 
v1 pod still there is a termination frace period which will enabel
to complete the requests that were already made to the particular pod before th
traffic to the v1 pod is cut down by load balancer.
If we make a update
