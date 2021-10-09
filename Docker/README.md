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
      
      i)   Clone a repo **git clone https://github.com/nigelpoulton/psweb.git**
      ii)  Go in the psweb folder, this is a basic node js web application
      iii) nano Dockerfile, to read the contents of Dockerfile
      iv)  Build docker image from the application code using **docker image build -t test:latest .**
      v)   Check newly build docker image using **docker image ls** , this image contains all the app code along with the dependencies
      vi)  Run a container using the docker image **docker container run -d --name web1 --publist 8080:8080 test:latest**
      vii) Open a web browser and navigate to the DNS name or IP address of the Docker host that you are running the container from,
           and point it to port 8080. You will see the a web page.
           
# Docker Engine

In many ways, the Docker Engine is like a car engine; both are modular and created by connecting many small specialized parts:
The Docker Engine is made from many specialized tools that work together to create and run containers, such as APIs, execution driver, 
runtimes, and shims, etc.
       
At the time of writing, the major components that make up the Docker engine are: the Docker daemon, containerd, runc, and various plugins, such as networking and storage. Together, these create and run containers.

![docker screenshot](https://user-images.githubusercontent.com/22169012/136653145-3f555275-c539-4f48-97f1-3d2a1c6f64b2.png)

## How a new container starts
   **docker container run --name ctr1 -it alpine:latest sh**
   
   When you type commands like this into the Docker CLI, the Docker client converts them into the appropriate API payload and POSTs them to the API endpoint exposed by the Docker daemon.

The API is implemented in the daemon and can be exposed over a local socket or the network. On Linux the socket is /var/run/docker.sock and on Windows it’s \pipe\docker_engine.

Once the daemon receives the command to create a new container, it makes a call to containerd. Remember that the daemon no-longer contains any code to create containers!

The daemon communicates with containerd via a CRUD-style API over gRPC.

Despite its name, containerd cannot actually create containers. It uses runc to do that. It converts the required Docker image into an OCI bundle and tells runc to use this to create a new container.

runc interfaces with the OS kernel to pull together all of the constructs necessary to create a container (namespaces, cgroups, etc.). The container process is started as a child-process of runc, and as soon as it is started, runc will exit.

Voila! The container is now started.

The process is summarized in the figure below
![docker screenshot 2](https://user-images.githubusercontent.com/22169012/136653456-5e5590fa-d4a7-4385-adfa-03eca6203e29.png)


