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

### HA vs Fault Tolerance vs DR
- **High Availabilty**
  - **High availability main objective is with maximizing the uptime** (making sure to maintain high operational time), minimizing the down time.
  - Can be accomplished with **spare capacity (physical or virtual resources)** and **automating things** (like to automatic spin up stand by server in case of main server failure).
  - Calculated in 9s (99.9, 99.999 %)
  -Examples
    - Having a spare tyre in car is like having HA, it does not guarantee it won't go down but if it does you can change the tire with very less downtime instead of waiting for help.
    - Having a standby server for an application in case of main server failure, the service will be down but instead of fixing the server first we simply switch to standby server, spin it up and it will take care of app.(Note: The down time will still be there but if we waited for fix on the main server it would have taken lot longer)

- **Fault Tolerance**
  - Fault tolerance deals with 2 things
    - Minimizing the downtime (same as HA)
    - **Tolerate failure** (levels of redundancy & system components that route session around failed components)
  - Fault tolerance means that despite having a fault the system should still work.
  - Example
    - Let's say if we have a critical hospital app that provides real time user heart condition to doctor during surgery in this case we won'use a standby server as even a small time disturbance or downtime can be critical & fatal
    - In the above case our health monitor will connect to two server both in active-active state, even if one fail the other one will provide data to the monitor.
    - A plane is example of system that need to be fault tolerant and not just Highly Available, think about a plane that fails for 15 mins in air, it would be fatal.
  - Harder to design, more costly and more complex implementation as compare to HA

- **Disaster Recovery**
  - a set of tools, policies and procedures to enable the recovery or continuity of vital technology and systems following a natural or human induced system disaster.
  - DR is about what to plan for and do in case of system failures (like fire in building or earthquake)

    
### Route 53
- Deals in 2 things
  - **Register Domains**
  - **Host zones and managed nameservers**
-  Global resiliant service (can tolerata failure of 1 or 2 regions, all regions needs to go down at global level for Route 53 to fail)
- Process of creating zone files & creating a number of nameservers, putting those zone files on those nameservers then liasing with registries for top level domains and getting nameserver records added on top level domain zone which point back at this servers. 

<img width="965" alt="Screenshot 2024-09-18 at 12 47 50 AM" src="https://github.com/user-attachments/assets/2053567e-650c-4b01-8c11-445f517e877f">


### DNS Record Types
- Nameserver
- A (www -> ipv4 address)
- AAAA (www -> ipv6 address)
- CNAME (link to other record type like A)
- MX (mail with priority no)
- TXT (text can be added)


## IAM, Accoints & AWS Organizations

### IAM Identity Policies
<img width="998" alt="Screenshot 2024-09-19 at 11 34 05 PM" src="https://github.com/user-attachments/assets/d5e900f9-e4c6-4f3a-a215-4b9b2b89fd72">

- When a user access a resource all 3 below permission are checked & all of the policies rules are combined and then decision is taken on basis of Explicit Deny, Explicit Allow and Implicit Deny (in this order only)
  - IAM User Policy
  - IAM Group Policy (If user is part of any group)
  - Resource Policy (This are written on Resources like S3/ EC2 and can only be assigned to IAM User or IAM Role using arn & not to IAM Group)
- Inline policy is when we create JSON and apply it to 3 users separately. (JSON has to be applied on all 3 accounts)
  - Exception case use when explicit permission  allow/deny for user.
- Managed Policies
  - To provide common access right to lot of people
  - Reusable & low management overhead
  - 2 types
    - AWS managed policy
    - custom managed policy

### IAM Users and ARN
<img width="998" alt="Screenshot 2024-09-20 at 2 19 05 AM" src="https://github.com/user-attachments/assets/9def248c-08b2-4ab8-9b4c-49c0f3fe5bf9">
<img width="998" alt="Screenshot 2024-09-20 at 2 19 45 AM" src="https://github.com/user-attachments/assets/566a8184-f2fa-4001-a207-1abe6aecf2fb">

- Principal is a person/ computers/ services/ application that needs to interact with AWS resources.

### IAM Groups
- Container of users (a user can be added into an IAM group)
- **Does not have** their own **credentials**, cannot login into IAM groups
- Used for easier management of IAM Users.
- Groups are not true identity they can't be referenced as a principal in policy, a resource policy cannot reference IAM group thus IAM group does not works for Resource policies.

<img width="998" alt="Screenshot 2024-09-26 at 3 16 56 AM" src="https://github.com/user-attachments/assets/06991092-387c-41dc-aec4-e890d79429b8">


### IAM Roles
<img width="854" alt="Screenshot 2024-09-26 at 4 11 49 AM" src="https://github.com/user-attachments/assets/cb603935-72a6-40e6-ab4c-f8849a12c360">

- STS (Secured Token Service AWS) creates temporary credentials for IAM roles.  
- IAM roles are used when no. of principals are not known  
  - n no of exteranl users/ application/ services will assume IAM role. Also casw where EC2 machines will require access to S3, but the EC2 machine numbers might change.  
  - **IAM roles are assumed**, you become that role for temporary period of time.  
- Trust poicy decide whether you are allowed to assume that role or not.  

### When to use IAM roles
- Instead of hardcoding credentials in lambda function (function as a service) we can use IAM role to make lambda assume role using sts:Assumerole (secured token service)
  - Avoid hardcoded access key and other credentials
  - No of lambdas that need to access particular s3 bucket could be 2,5 or 20 we don't know the exact number as we can run n no of lambda functions we are using IAM role. 

<img width="1021" alt="Screenshot 2024-09-26 at 4 16 13 AM" src="https://github.com/user-attachments/assets/0ff49d82-d7d4-4590-9c6b-b3b2db01e390">

<img width="1022" alt="Screenshot 2024-09-26 at 4 18 57 AM" src="https://github.com/user-attachments/assets/8957e313-a8a3-4cd7-ac32-64df618792d9">

### Service-linked Roles & PassRole
<img width="1013" alt="Screenshot 2024-09-27 at 4 18 35 AM" src="https://github.com/user-attachments/assets/1b5c3044-c444-4ec3-9976-44b16f58069b">



### Service Control Policies
<img width="1022" alt="Screenshot 2024-09-26 at 4 45 25 PM" src="https://github.com/user-attachments/assets/8e671320-aedb-4e56-83d0-ed0c0c0fe93f">

- Service Control Policies are **account permission boundaries**
- SCP can be attached to whole organization (root container), individual AWS service account or Organization Unit.
- **SCP permissions trickle downs**, if we attach SCP to an Organization unit then all the accounts within that OU and all the aws member accounts will also impacted.
- **Management account** (payer account of AWS organization) is special even if we attach the SCP (service control policies) on root container the **SCP will not impact the management account**.
- SCP don't grant permissions, they just limit the permission that can be assigned to a aws account (in the organization).
- By **default** SCP provide **FullAWSAcess** policy (that means no restriction)
- Rule for assesment
  - Explicit Deny
  - Explicit Allow
  - Implicit Deny

<img width="1022" alt="Screenshot 2024-09-26 at 4 48 25 PM" src="https://github.com/user-attachments/assets/e1c304c6-cf8f-48b2-9363-9f5742582bfb">

  
