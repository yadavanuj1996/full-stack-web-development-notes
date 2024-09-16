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

### S3 (Simple Storage Service)
- Global storage service provided by AWS (present across the world)
- S3 is **region resiliant** (Failure of AZ does not affect S3 service)
- S3 is public service of aws (part of aws public network)
  - Should be first go to service for storing data (text, large data sets, video etc)

<img width="1026" alt="Screenshot 2024-09-15 at 4 49 10 AM" src="https://github.com/user-attachments/assets/411c886b-e3d3-42e5-ab9a-7bcdfa35764e">

- S3 contains bucket and object
  - Object contains (only two item mentioned here rest are omitted for now)
    - key
    - value
    - **size of object can vary from 0 bytes to 5 TB.**
  - S3 Bucket
    - **S3 bucket name should be Globally Unique**
      - needs to be unique across all aws accounts (two aws user cannot have same s3 bucket name)
    - can contain unlimited ojects
    - flat structure ( all objects are stored as same level)
      - UI does present it as folder structure but it's only for display, let's say if we store /old/koala1.jpg, then s3 treat **/old/** part as prefix and the folder structure is only for display the objects are stored in flat manner

 <img width="1026" alt="Screenshot 2024-09-15 at 4 41 44 AM" src="https://github.com/user-attachments/assets/548fa270-ff62-4682-a6f3-7f26c8551e48">

### Cloud Formation (CFN)
- Cloud Formation is used to create, update or delete infrastructure (instead of doing it manually)
- CFN use template to update infrastructure (format: YAML or JSON), CFN is Infrastructure as Code.
- Allow Automated consistent provisioning, apply same template will always give same result
- Helps us manage infrastructure easily
- Mainly works around 2 items
  - template (logical resources, contain details and conditions)
  - stack (physical resources)
  - CFN make sure logical and physical logic is **in sync**.

  <img width="904" alt="Screenshot 2024-09-16 at 11 55 40 PM" src="https://github.com/user-attachments/assets/b1db9beb-59b8-4027-8524-32294dc30b9c">

### CloudWatch
- Mainly does 3 things
  - Metrics Tracking (AWS product, apps, on premise)
    - Disk usage on on premise, no of visits on app, metric of aws service  
  - CloudWatch logs
    - Auto generate aws service logs, app and other logs can be ingested on it
  - Cloud Watch Events
    - AWS services
      - EC2 Machine started, stopped, terminated will generate event that can create new action (like sending mail - like budget cross mail)
    - Schedule
      - Create and run an action at a fixed time in aws
  - Namespaces are containers that are used to keep a certain type of metrics uncluttered from other metrics
  - Metrics are series of values in an time ordered manner.
  - Within a namespace an Dimension is used to keep differentiation between two same type of entity sending metrics
    - Ex: using dimension we can check value of two different EC2 machine CPU usage, while in the namespace we will be getting overall CPU usage. 
  
<img width="924" alt="Screenshot 2024-09-17 at 2 01 49 AM" src="https://github.com/user-attachments/assets/eff3f476-bd3b-4995-b73d-953931573e1b">

