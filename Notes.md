# AWS CLOUD PRACTITIONER STUDY MATERIALS
- [AWS CLOUD PRACTITIONER STUDY MATERIALS](#aws-cloud-practitioner-study-materials)
  - [1: Introduction to AWS](#1-introduction-to-aws)
    - [Introduction](#introduction)
    - [Cloud Computing](#cloud-computing)
      - [Deployment models for cloud computing](#deployment-models-for-cloud-computing)
      - [Benefits of Cloud Computing](#benefits-of-cloud-computing)
  - [2: Compute in the Cloud](#2-compute-in-the-cloud)
    - [Introduction](#introduction-1)
      - [Amazon Elastic Compute Cloud (Amazon EC2)](#amazon-elastic-compute-cloud-amazon-ec2)
    - [Amazon EC2 Instance Types](#amazon-ec2-instance-types)
    - [Amazon EC2 Pricing](#amazon-ec2-pricing)
    - [Scaling EC2](#scaling-ec2)
      - [Scalability:](#scalability)
    - [Directing Traffic with Elastic Load Balancing](#directing-traffic-with-elastic-load-balancing)
    - [Messaging and Queueing](#messaging-and-queueing)
      - [Monolithic Applications vs Microservices](#monolithic-applications-vs-microservices)
    - [Additional Compute Services](#additional-compute-services)
  - [3: Global Infrastructure and Reliability](#3-global-infrastructure-and-reliability)
    - [AWS Global Infrastructure](#aws-global-infrastructure)
    - [Edge Locations](#edge-locations)
    - [How to Provision AWS Resources](#how-to-provision-aws-resources)
      - [AWS Management Console](#aws-management-console)
      - [AWS CLI](#aws-cli)
      - [Software Development Kits](#software-development-kits)
      - [AWS Elastic Beanstalk](#aws-elastic-beanstalk)
      - [AWS CloudFormation](#aws-cloudformation)
  - [4. Networking](#4-networking)
    - [Intro](#intro)
      - [Amazon Virtual Private Cloud](#amazon-virtual-private-cloud)
    - [Connectivity to AWS](#connectivity-to-aws)
      - [Internet gateway](#internet-gateway)
      - [Virtual Private Gateway](#virtual-private-gateway)
      - [AWS Direct Connect](#aws-direct-connect)
    - [Subnets and Network Access Control Lists](#subnets-and-network-access-control-lists)
      - [Subnets](#subnets)
      - [Netwrok Traffic in a VPC](#netwrok-traffic-in-a-vpc)
      - [Network Access Control List (ACL)](#network-access-control-list-acl)
      - [Stateless Packet Filtering](#stateless-packet-filtering)
      - [Security Groups](#security-groups)
      - [Stateful Packet Filtering](#stateful-packet-filtering)
    - [Global Networking](#global-networking)
      - [Domain Name System (DNS)](#domain-name-system-dns)
      - [Amazon Route 53](#amazon-route-53)
  - [5. Storage and Databases](#5-storage-and-databases)


## 1: Introduction to AWS

### Introduction

- Client-server model

- Server: Amazon Elastic Compute Cloud (Amazon EC2)
  - validates requests
  - returns repsonse

- You only pay for what you use with AWS.
  - So essentially, pay for what you need.

### Cloud Computing

- <b>Definition</b>: The on-demand delivery of IT resources over the internet with pay-as-you-go pricing.
- Undifferentiated heavy lifting of IT. Common tasks expected of all IT solutions.
  
#### Deployment models for cloud computing

- Companies have varying IT infrastructure requirements
- There are 3 cloud computing deployment models:
  - <b>Cloud-Based Deployment</b>:
    - Run all parts of the application in the cloud.
    - Migrate existing applications to the cloud.
    - Design and build new apps in the cloud.
    - New apps can be built using low-level infrastructure that a company manages on their own, or using high-level infrastructure constructed and managed by AWS.
  - <b>On-Premises Deployment</b>:
    - Maintain applications that are run on technology that is fully kept on-premises.
    - Deploy them using virtualization and resource management tools.
    - Increases resource utilization by using application management and virtulaization technologies.
  - <b>Hybrid Deployment</b>:
    - Allows the maintaining of legacy applications on-premises while still making use of the cloud-based resources.

#### Benefits of Cloud Computing
- Trade upfront expense for variable expense
- Stop spending money to run and maintain a data-center
- Stop guessing capacity because AWS offers scalabality as you need it.
- Cheaper rates because large clouds achieve higher economies of scale. 
- Speed and agility of cloud computing.
- AWS's global footprint allows you to quickly deploy globally with low latency.

------------------

## 2: Compute in the Cloud

### Introduction

- Multitenancy: Sharing underlying hardware between virtual machines.
- Hypervisor: Divides virtual machines.
- EC2 instances are unaware of eachother.
- EC2 Config:
  - Can choose OS
  - Can choose whatever software you want to run on your EC2 instance.
    - includes DBs
    - Web apps
  - Vertically scaling: Increase CPU and storage.
  - Control network accessability. 
  - Compute as a Service (CaaS).

#### Amazon Elastic Compute Cloud (Amazon EC2)

- Launch: Select a template with basic configs like those listed above. Includes specifying network security.
- Connect: Can connect in many ways via a program or app. Users can also access the instance by logging in and accessing the computer desktop.
- Use: After you connect. You can install software, add storage, and copy and organize files.


### Amazon EC2 Instance Types

- EC2 instances are like employees at a coffee shop. They all handle certain requests with a variety of tasks.
- Different types of employees -- Different types of instances
- Divided into different families with different configs of cpu, memory, and storage.
- Types
  1. ##### General purpose
    - Balance of compute, memory and networking resources.
    - Can be used for application servers, gaming servers, backend servers for enterpirse applications, or small and medium databases.
    - <b>Consider:</b> Cases where the need for computing, memory, and networking are relatively equivalent.
  2. ##### Compute optimized
    - Compute intensive tasks
    - gaming servers, high performance computing (HPC), and scientific modeling, batch processing.
    - <b>Consider:</b> Can the product benefit from high computing capabalities like batch processing workloads that need to process a lot at once.
  3. ##### Memory Optimized
   - Memory intensive tasks
   - <b>Consider:</b> Cases where large amounts of data need to be loaded into memory at once. For example, a high perfomance database that stores data in memory for quick access.
  4. ##### Accelerated computing
    - floating point number calculations, graphics processing, data pattern matching
    - Utilize hardware acceleration. Hardware accelerators expedite data processing.
  5. ##### Storage optimized
    - Storage intensive tasks
    - Examples: distributed file systems, data warehousing applications, and high-frequency online transaction processing systems
    - <b>IOPS</b> - input/output operations per second
    - <b>Consider:</b> Applications that have high IOPS requirements.

### Amazon EC2 Pricing

- Purchase Options
  1. On-Demand
   - Ideal for short-term, irregular workloads that can't be interrupted.
   - Examples: Developing/testing apps, runnings apps with unpredicatble usage patterns
  2. Savings Plans
   - Commit to an hourly rate to an instance family and Region for 1 or 3 year term.
   - So its still pay as you use (meaning you don't need to specify anything upfront) but you do commit to a rate up front.
   - Savings up to 72% compared to on-demand.
  3. Reserved Instances
   - A billing discount applied to the use of On-Demand instances in your account. 
     - Strandard Reserved Instances: Specify your instance type and size and region before buying.
     - Convertible Reserved Instances: Good if you need to change to different availability zones or instance types.
   - Reserved instances require that you state the following:
     1. Instance type and size: m5.xlarge
     2. Platform description (OS)
     3. Tenancy
   - After the term is over, you revert to On-Demand pricing until you specify to either terminate the instance or purchase a new reserved instance. 
  4. Spot Instances
     - Uses unused EC2 computing capacity but can be interrupted at any time. Basically mooching. Good for processing that is in no rush.
  5. Dedicated Hosts
     - Physical servers with Amazon EC2 instance capacity that are fully dedicated to your use. 
     - Most expensive.

### Scaling EC2

How capacity can grow and shrink based on business needs. Want a full system with no single point of failure.

#### Scalability:

- Involves beginning with only the resources you need and designing your architecture to automatically respond to changing demand by scaling out or in. 
- The <b>Amazon EC2 Auto Scaling</b> enabled you to automatically add or removes instances in repsonse to changing application demand.
- Two approaches:
  - <i>Dynamic Scaling</i> responds to changing demand.
  - <i>Predictive Scaling</i> automatically schedules the right number of instances based on predicted demand.
- Decoupled system allows for exactly the right amount of power for each instance type.
  - Like if you only needed 3 coffee makers but 8 order takers.
- Can set a minimum capacity, desired capacity, and a max capacity.

### Directing Traffic with Elastic Load Balancing

Need to organze the workload evenly among the instances. Need a host. Called a <b>Load Balancer</b>

<b>Elastic Load Balancing</b>:

- Regional construct, so it is readily available with no added cost.
- ELB also acts as a middle man between different tiers (instance types).
- When an instance is ready, it tells the ELB. When an instance is terminating, it tells the ELB.

![Auto Scaling](Auto-Scaling.png)

### Messaging and Queueing

Like an order board. Queues orders to the barista so they don't have to vbe perfectly in sync. (Five white boys but theyre not insync)

**Loosely-coupled architecture** : Applications failure does not cascade.

- Amazon Simple Queue Service (SQS):
  - Send
  - Store
  - Receive
  - Messages between software components at any volume.
  - Order board is SQS queue
  - Data contained within a message is called a **Payload**
- Amazon Simple Notification Service
  - Used to send out messages and notifications.
  - Notifications are publish/subscribe modal.
  - Can fan out notifications to users and instances.

#### Monolithic Applications vs Microservices

Monolithic Apps are composed of multiple tightly-coupled components.

Microservices approach allows for loosely coupled components. In AWS, the microservice approach is achieved using two services to achieve application integrationg: Amazon SNS, and Amazon SQS.

### Additional Compute Services

- **Serverless:** You cannot see or access the underlying infrastructure.
  - Gives you more time to worry about new products and developments rather than maintaining servers.
  - **AWS Lambda:** Put code into a lambda function and set up a trigger to know when to use that function. 
    1. Upload Code to Lambda.
    2. Set Code to trigger from an event source.
    3. Code runs only when triggered.
    4. Pay only for the compute time you use. 
    - Processes under 15 minutes.
- **Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS).**
  - Container orchestration tools:
    - Created to help you manage your containers.
  - Container: A package for you code including dependencies and configs.
  - ECS designed to run containerized apps at scale. Supports Docker.
  - EKS does similar thing but with different tooling and features.
- **AWS Fargate** manages your containerized apps for you.


## 3: Global Infrastructure and Reliability

Need high availability and fault tolerance. AWS operates in many different areas called **Regions**

### AWS Global Infrastructure

- Choose which region you want to run out of
  - Regions are closed ecosystems.
- Business Factors for choosing a Region
  1. Compliance: Could be legal
  2. Proximity: How close can you get to your customer base.
     - **Latency** is a big factor
  3. Feature availabilty: Some regions do not have full availability of all features of AWS. Always changing.
  4. Pricing: Some regions are more costly to run out of than others. This can due to laws. Each region has a different price sheet. 

- Each **Availability Zone** or Zed is one or more discrete data centers with redundant everything.
- EC2 instances launch a virtual machine on a physical hardware that is intalled in an availability zone
- **Each AWS Region consists of multiple isolated Availability Zones**
- They aren't built right next to eachother in case of disaster.
- Referring back to AWS Scaling. When maintaining multiple instances of the same type (to account for failure) they are run from different availability zones within the Region. 

![Regions](Regions-Zeds.png)

### Edge Locations

- **CDN**: Content Delivery Network

- **Amazon Cloud Front**: Amazon CDN
  - Uses "edge locations". 
  - Push content from a region to edge locations to speed up responses.
- **AWS Outposts**: Install a AWS Region within your own data center.

### How to Provision AWS Resources

- In AWS everything is an API.

#### AWS Management Console

- Web based interface for accessing and managing AWS services
- Can be used on mobile to monitor resources, view alarms, and access billing info.

#### AWS CLI

- Make AWS API calls in the AWS command line interface

#### Software Development Kits

- AWS SDKs allow you to make API calls for your desired programming language.
- Supported languages include: C++, Java, .NET, and more. (Probably JS)

#### AWS Elastic Beanstalk

- Provide code and config settings and Elastic Beanstalk deploys the resources necessary to perform:
  - Adjust capacity
  - Load balancing
  - Automatic scaling
  - Application health monitoring

#### AWS CloudFormation

- Allows you to define resources declaritively using JSON or YAML. 
- Lets you define what you want.
- Supports many AWS services.
1. Create **CloudFormation Template**
2. CloudFormation parses the tmplate and provision the resources you defined
3. CloudFormation manages all API calls for you. 

## 4. Networking

### Intro

#### Amazon Virtual Private Cloud

Creates isolated section in cloud.

- Can be public-facing
- Or private, with no internet access
- Called subnets
- Cashier would be in public subnet
- Barista in private subnet

### Connectivity to AWS

- **VPC** is used to establish boundaries around your AWS resources.
  - Allows you to provision an isolated section of AWS cloud where you can launch resources in a virtual network.

#### Internet gateway
- Allows public traffic from the internet into your VPC

#### Virtual Private Gateway
- To access private resources in a VPC, use a **Virtual PRivate Gateway**
- Allows protected interent traffic to enter the VPC.
- "Protected" Internet Traffic is traffic encrpyted using a VPN

![VPNxVPG](VPG&VPN.png)

#### AWS Direct Connect

- Allows for a direct and private connection between a data center and VPC.
- Helps reduce network costs and increase the amount of bandwidth that is available for other requests to travel through your network.

### Subnets and Network Access Control Lists

#### Subnets

A private section of a VPC in which you can group resources based on security or operational needs. Can be public or private
- **Public Subnets** Contain resources that need to be accessed by the public
- **Private Subnets** Contain resources that should only be accessible through your private network, such as a database that contains personal info
- Subnets can communicate with eachother. Part of the decoupled system.

#### Netwrok Traffic in a VPC

- A **Packet** is a unit of data sent over the internet or a network
- Netwrok traffic enters into a VPC through an internet gateway.
- Before a packet enters into a subnet it must be checked for permissions.

#### Network Access Control List (ACL)

Controls inbound and outbound traffic at a subnet level.
- The default Network ACL allows all in/out traffic into subnets.

#### Stateless Packet Filtering

- Remember nothing
- abide by a list.
- Checks list to enter and exit
- Network ACL's are stateless

#### Security Groups

- Virtual firewall that controls inbound and outbound traffic for an EC2 instance
- Default: Allows all outbound, denies all inbound.
- If multiple instances in a VPC, they can either share a security group or have their own.

#### Stateful Packet Filtering

- Security Groups are stateful.
- They remember previous decisions made for incoming packets.
- Remembers responses from requests they sent.

### Global Networking

#### Domain Name System (DNS)

The phone book of the internet.

- Client connects to DNS resolver looking for a domain
- Resolver asks company DNS server for IP Address
- The company DNS server responds with the IP.
  
#### Amazon Route 53

- Gives a reliable way to route end users to internet applications hosted in AWS
- Also allows you to manage all of your domain names in one place.


## 5. Storage and Databases




