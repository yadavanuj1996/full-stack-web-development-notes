# Cantrill Solution Architect course (SA-C03)

## AWS fundamentals

### IAM (Identity & Access Management)
- IAM is free and replicated across all regions (global service)
- IAM lets you create 3 different identity objects
  - IAM User: Used for a person or a application 
  - IAM Group: Group can have policies and user can be placed in a group 
  - IAM Role: Can be used by AWS services
    - Ex: all EC2 instances needs to access S3 (Simple Storage Service) then we create a IAM role provide permission and allow instance of EC2 to access that service using the role.
    - If no of things are uncertain- ex we need to provide external accounts to access S3, we need to provide uncertain no of EC2 instance access S3 services.
- Three tasks:
  - Manage Identites (also provides identities)
  - Authenticate
  - Authorize  

<img width="1026" alt="Screenshot 2024-09-15 at 2 18 43 AM" src="https://github.com/user-attachments/assets/3d31fc08-76b7-4bca-ae3f-0327e24d8f38">

### AWS Public vs Private Services
<img width="1020" alt="Screenshot 2024-09-15 at 2 09 35 AM" src="https://github.com/user-attachments/assets/0be19fe0-d20a-4b3f-bce3-45cb52b266a7">

### Regions, AZs and edge points
- AWS services are provided in multiple regions distributed across the globe
- Each region contains multiple AZs (Avilability Zones)
- Egde location: A site that AWS uses to cache copies of your content for faster delivery to users at any location, ex: Netflix case.

<img width="635" alt="Screenshot 2024-09-15 at 2 10 39 AM" src="https://github.com/user-attachments/assets/0508763e-9555-43f1-a952-3954dacefb92">

### VPC (Virtual Private Cloud)
- VPC is **virtual network** in aws cloud, that is in private network zone of AWS & is private and isolated (unless you provide it permission to conntect to public internet via Internet Gateway which is in turn part of public aws service)
- VPC is withing one aws account and in one region, each Availability Zone of the region will contain one subnet of VPC thus making VPC region resistant.
- Each subnet is assigned with a particular range of IP addresses (that are public IPv4) that is provided/associated with the VPC.
- Each AWS account has a default VPC with fixed IP address range and we can create multiple Custom VPC for a region (generally used for prod env)
- VPCs are also used to connect AWS private network to connect with your on-premise network
- We can delete a default VPC as well, but it is not advised as some services of aws work on the assumption that default VPC is present.

<img width="887" alt="Screenshot 2024-09-15 at 2 06 36 AM" src="https://github.com/user-attachments/assets/71ee4a28-0850-4a0f-9b02-9a048908cfc1">


### EC2 (Elastic Compute Cloud) Basics
- EC2 is IAAS, it proides virtual machines (you can install OS on it depending on requirement)
- EC2 is private aws service (private aws netword zone) & EC2 instance is configure to launch in a single VPC subnet.
  - VPC needs to support public support if we need to make EC2 instance public access.
- EC2 is AZ resistant, as a EC2 instance is launched in one VPC subnet.
- EC2 instance has
  - CPU
  - memory
  - storage
    - Local on-host storage (instance of EC2 host runs on itself)
    - EBS (Elastic Block Storage) , network storage made available to intance.
  - Addition software
- Few common states (only three are mentioned here)
  -  Running
  -  Stopped
  -  Terminated
- AMI is used to create EC2 instances (also an AMI can be created from an EC2 instance)

<img width="1026" alt="Screenshot 2024-09-15 at 3 30 34 AM" src="https://github.com/user-attachments/assets/b8dd92a2-0475-427f-acbf-9961b8990040">
