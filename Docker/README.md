# DOCKER Technology and Commands

## Installation
   Simply download Docker Desktop on your local system from Docker Website,

## 1. Docker Technology consists of 3 items:
   ### i) The runtime
    The runtime operates at the lowest level and is responsible for starting and stopping containers (this includes building all of the OS
    constructs, such as namespaces and cgroups). Docker implements a tiered runtime architecture with high-level and low-level runtimes
    that work together.
    Runtime Contains: 
     a) runc (one per running container
      The low-level runtime is called runc and it is the reference implementation of Open Containers Initiative (OCI) runtime-spec. 
      Its job is to interface with the underlying OS and start and stop containers. Every running container on a Docker node has a runc
      instance managing it.
     b) containerd
      The higher-level runtime is called containerd. containerd does a lot more than runc. It manages the entire lifecycle of a container, 
      including pulling images, creating network interfaces, and managing lower-level runc instances.
   ### ii) Docker Daemon/ Docker Engine
    The Docker daemon (dockerd) sits above containerd and performs higher-level tasks, such as exposing the Docker remote API, 
    managing images, managing volumes, managing networks, and more.
   ### iii) Docker Swarn (Orchestrator)
      Docker also has native support for managing clusters of nodes running Docker. These clusters are called “swarms” and the native
      technology is called “Docker Swarm.

## 2. Docker Commands

### i) docker version
      To check if docker is installed, If you get a response back from the Client and Server, you’re good to go.
      
### ii) What are Docker images?#
   It’s useful to think of a Docker image as an object that contains an OS filesystem, an application, and all application dependencies.
   
   If you work in operations, it’s like a virtual machine template. A virtual machine template is essentially a stopped virtual machine.
   In the Docker world, an image is effectively a stopped container. If you’re a developer, you can think of an image as a class.
   
### iii) docker image ls
         To list all pulled docker images
    
### iv) docker image pull ubuntu:latest
         To pull the docker image- latest version of ubuntu
         
### v) docker container run
         To run a docker container
         
####     docker container run -it ubuntu:latest /bin/bash

   This command will run the latest image of ubuntu and start the bash inside the container, the -it flag will switch the shell to terminal 
   of the container.

   Look closely at the output from the previous commands. You should notice that the shell prompt has changed in each instance. 
   **This is because the -it flags switch your shell into the terminal of the container**; you are literally inside of the new container!

   The ** ps -elf ** command/process that we ran to list the running processes.

   **Press Ctrl + PQ** for exiting the terminal of container and coming back to shell. 
         
   **We can also start a container with docker service create**         
         
### vi) docker container ls
         To list all the running containers
         
### vii) docker container exec -it running_container_name bash

   exec is used to Run a command in a running container

   we used the -it options to attach our shell to the container’s shell

   You can attach your shell to the terminal of a running container with the **docker container exec** command. 
   We can make a connection to one of the running containers.

### viii) docker container stop running_container_name
      To stop a running container
      run docker container ls and the container will not display now as it is stopped

      although if we run docker container ls -a command we can see the entry of that container in **Exited** status

### ix) docker container rm epic_jones
      To remove a stopped container 
      Even on docker container ls -a, no entry of the container would be present

### x) docker image build

   **docker image build -t test:latest .**
   Use the docker image build command to create a new image using the instructions in the Dockerfile. This example 
   creates a new Docker image called test:latest.       
   
   ```
   i)   Clone a repo **git clone https://github.com/nigelpoulton/psweb.git**
   ii)  Go in the psweb folder, this is a basic node js web application
   iii) nano Dockerfile, to read the contents of Dockerfile
   iv)  Build docker image from the application code using **docker image build -t test:latest .**
   v)   Check newly build docker image using **docker image ls** , this image contains all the app code along with the dependencies
   vi)  Run a container using the docker image **docker container run -d --name web1 --publist 8080:8080 test:latest**
   vii) Open a web browser and navigate to the DNS name or IP address of the Docker host that you are running the container from,
        and point it to port 8080. You will see the a web page.
   ```

### xi) docker image rm image_name
   To delete a Docker image
   
# Docker Engine

   In many ways, the Docker Engine is like a car engine; both are modular and created by connecting many small specialized parts:
   The Docker Engine is made from many specialized tools that work together to create and run containers, such as APIs, execution driver, 
   runtimes, and shims, etc.

   At the time of writing, the major components that make up the Docker engine are: the Docker daemon, containerd, runc, and various
   plugins, such as networking and storage. Together, these create and run containers.

   ![docker screenshot](https://user-images.githubusercontent.com/22169012/136653145-3f555275-c539-4f48-97f1-3d2a1c6f64b2.png)

## How a new container starts
   **docker container run --name ctr1 -it alpine:latest sh**
   
   When you type commands like this into the Docker CLI, the Docker client converts them into the appropriate API payload and POSTs
   them to the API endpoint exposed by the Docker daemon.

   The API is implemented in the daemon and can be exposed over a local socket or the network. On Linux the socket is /var/run/docker.sock 
   and on Windows it’s \pipe\docker_engine.

   Once the daemon receives the command to create a new container, it makes a call to containerd. Remember that the daemon no-longer contains any code to create containers!

   The daemon communicates with containerd via a CRUD-style API over gRPC.

   Despite its name, containerd cannot actually create containers. It uses runc to do that. It converts the required Docker image into an OCI bundle and tells runc to use this to create a new container.

   runc interfaces with the OS kernel to pull together all of the constructs necessary to create a container (namespaces, cgroups, etc.). The container process is started as a child-process of runc, and as soon as it is started, runc will exit.

   Voila! The container is now started.

   The process is summarized in the figure below
   ![docker screenshot 2](https://user-images.githubusercontent.com/22169012/136653456-5e5590fa-d4a7-4385-adfa-03eca6203e29.png)

**Run Docker Daemon and Docker Client with TLS in Production env for security purposes**


# Docker Images

   A Docker image is a unit of packaging that contains everything required for an application to run. This includes: application code,
   application dependencies, and OS constructs. If you have an application’s Docker image, the only other thing you need to run that 
   application is a computer running Docker.

   Docker image is like a stopped container. If you’re a developer you can think of them as similar to classes as, they are like blueprint
   of a container.

   You get Docker images by pulling them from an image registry. The most common registry is Docker Hub, but others exist. The pull operation downloads 
   the image to your local Docker host where Docker can use it to start one or more containers.

   Images are made up of multiple layers that are stacked on top of each other and represented as a single object. Inside of the image is 
   a cut-down operating system (OS) and all of the files and dependencies required to run an application. Because containers are intended 
   to be fast and lightweight, images tend to be small.

   Images are considered build-time constructs, whereas containers are run-time constructs.

    Once you’ve started a container from an image, the two constructs become dependent on each other, and you cannot delete the image until 
    the last container using it has been stopped and destroyed. Attempting to delete an image without stopping and destroying all containers
    using it will result in an error.

   The image also doesn’t contain a kernel; all containers running on a Docker host share access to the host’s kernel. For these reasons,
   we sometimes say images contain “just enough operating system” (usually just OS-related files and filesystem objects).


## Docker Registries

   **Docker Registries is to docker image what the code Github is to Code Repositories**
   We store images in centralized places called image registries. This makes it easy to share and access them.
   The most common registry is Docker Hub. 

   If you want to pull images from 3rd party registries (not Docker Hub), you need to prepend the repository name with the DNS name of the registry. For example, the following command pulls the 3.1.5 image from the google-containers/git-sync repo on the Google Container Registry (gcr.io).

**docker image pull gcr.io/google-containers/git-sync:v3.1.5**

## Docker search and limit
docker search alpine   (To search alpine)
docker search alpine --filter "is-official=true" (You can use --filter "is-official=true" so that only official repos are displayed, alternate: is-automated=true)


A Docker image is just a bunch of loosely-connected read-only layers with each layer comprising one or more files. This is shown below.

### docker image inspect ubuntu:latest
     To inspect docker image
    
### docker history
   The docker history command is another way of inspecting an image and seeing layer data. However, it shows the build history of an 
   image and is not a strict list of layers in the final image
   
### docker image ls --digests alpine
   To list the digest (hash of image) along with other details about docker image

   Take a moment to consider what happened there; you have an image called golftrack:1.5 that has a bug. That image is being used by 
   containers in your production environment. You create a new version of the image that includes a fix. Then comes the mistake; you 
   build and push the fixed image back to its repository with the same tag as the vulnerable image! This overwrites the original image 
   and leaves you without a great way of knowing which of your production containers are using the vulnerable image and which are using
   the fixed image. They both have the same tag!
   This is where image digests come to the rescue.
   
   Command to delete and pull alpine image using digest
   ```
   docker image rm alpine:latest
   docker image pull alpine@sha256:9a839e63da...9ea4fb9a54
   ```

### docker manifest inspect
### docker buildx

