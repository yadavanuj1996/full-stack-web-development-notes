# DOCKER

## 1. Docker Technology consists of 3 items:
   ### i) The runtime
    The runtime operates at the lowest level and is responsible for starting and stopping containers (this includes building all of the OS
    constructs, such as namespaces and cgroups). Docker implements a tiered runtime architecture with high-level and low-level runtimes
    that work together.
    Runtime Contains: 
    #### a) runc (one per running container
      The low-level runtime is called runc and it is the reference implementation of Open Containers Initiative (OCI) runtime-spec. 
      Its job is to interface with the underlying OS and start and stop containers. Every running container on a Docker node has a runc
      instance managing it.
    #### b) containerd
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
       
