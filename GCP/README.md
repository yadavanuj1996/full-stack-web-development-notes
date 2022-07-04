## GCP


### To add docker iamge in GCR (Google Container Registry)
- To push images to your private registry hosted by gcr, you need to tag the images with a registry name. The format is [hostname]/[project-id]/[image]:[tag].
- For gcr:
  - [hostname]= gcr.io
  - [project-id]= your project's ID
  - [image]= your image name
  - [tag]= any string tag of your choice. If unspecified, it defaults to "latest".
- To fetch your project name 
  - gcloud config list project
- Tag docker image
  - docker tag node-app:0.2 gcr.io/[project-id]/node-app:0.2
- [hostname]/[project-id]/[image]:[tag]
- Push docker image
  - docker push gcr.io/[project-id]/node-app:0.2
- Pull docker image
  - docker pull gcr.io/[project-id]/node-app:0.2



### To Create a new cluster and deploy a application using docker image 
- To list the current project
  - gcloud config list project
- Set a default compute zone
  - gcloud config set compute/zone us-central1-a
- Create a GKE cluster
  - gcloud container clusters create [CLUSTER-NAME]
- Get authentication credentials for the cluster
  - gcloud container clusters get-credentials [CLUSTER-NAME]
  - kubectl config view to check the config
- Deploy an application to the cluster
  - kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
  - GKE uses Kubernetes objects to create and manage your cluster's resources. Kubernetes provides the Deployment object for deploying stateless applications like web servers. Service objects define rules and load balancing for accessing your application from the internet.
  - We have created a new Deployment hello-server from the hello-app container image using kubectl create command.
- To create a Kubernetes Service
  - kubectl expose deployment hello-server --type=LoadBalancer --port 8080
  - --port specifies the port that the container exposes.
  - type="LoadBalancer" creates a Compute Engine load balancer for your container
- To check all services
  - kubectl get services
- To view the application from your web browser, open a new tab and enter the following address, replacing [EXTERNAL IP] with the EXTERNAL-IP for hello-server.
  - http://[EXTERNAL-IP]:8080
- Deleting the cluster
  - gcloud container clusters delete [CLUSTER-NAME]



#### Create Cluster with specifying no of nodes
- gcloud container clusters create bootcamp --num-nodes 5 --scopes "https://www.googleapis.com/auth/projecthosting,storage-rw"
