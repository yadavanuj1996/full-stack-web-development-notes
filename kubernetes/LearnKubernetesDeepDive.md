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
 
