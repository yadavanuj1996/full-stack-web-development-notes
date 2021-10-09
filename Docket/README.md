# DOCKER Technology and Commands

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
      
         The **ps -elf** command/process that we ran to list the running processes.
         
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
         Even on docker container rm epic_jones
        
       
