# EC2 Overview

## Topic Overview

Amazon EC2 (Elastic Compute Cloud) is AWS's Infrastructure as a Service (IaaS) offering that provides resizable virtual servers in the cloud.

Before cloud computing, organizations had to purchase physical servers, provision data centers, manage hardware failures, and estimate future capacity requirements. EC2 eliminates these challenges by allowing users to launch virtual machines on demand within minutes.

EC2 provides:

* Virtual servers (instances)
* Flexible compute capacity
* Multiple operating systems
* Pay-as-you-go pricing
* Integration with other AWS services

---

## Why EC2 Exists

Traditional infrastructure introduces several challenges:

* High upfront hardware costs
* Long procurement cycles
* Capacity planning difficulties
* Hardware maintenance responsibilities
* Limited scalability

EC2 solves these problems by providing:

* On-demand server provisioning
* Rapid scalability
* Global deployment capabilities
* Flexible pricing models
* Managed physical infrastructure

---

## Problems EC2 Solves

### Infrastructure Procurement Delays

Instead of waiting weeks or months for hardware delivery, servers can be launched in minutes.

### Capacity Planning Challenges

Organizations can scale resources up or down as demand changes.

### Hardware Maintenance

AWS manages:

* Physical servers
* Networking equipment
* Power infrastructure
* Cooling systems
* Hardware replacements

### Global Deployment

Applications can be deployed across multiple AWS Regions worldwide.

---

## Real-World Use Cases

### Web Hosting

Hosting websites and web applications.

Examples:

* Company websites
* E-commerce platforms
* SaaS applications

### Application Servers

Running backend services.

Examples:

* Java applications
* Node.js applications
* Python APIs
* Microservices

### Database Servers

Hosting self-managed databases.

Examples:

* MySQL
* PostgreSQL
* MongoDB

### Development Environments

Providing isolated environments for developers and testers.

### Batch Processing

Running scheduled workloads and computational jobs.

### CI/CD Infrastructure

Hosting:

* Jenkins servers
* GitLab runners
* Build agents

---

# Core Concepts

## Instance

An EC2 instance is a virtual machine running in AWS.

Example:

```text
Ubuntu Server
4 vCPU
8 GB RAM
100 GB EBS
```

AWS provides the physical server.

You manage the operating system and applications.

---

## Amazon Machine Image (AMI)

An AMI acts as a server template.

It contains:

* Operating System
* Pre-installed software
* Configuration settings

Examples:

* Ubuntu 24.04
* Amazon Linux 2023
* Red Hat Enterprise Linux

---

## Instance Type

Defines hardware characteristics.

Examples:

```text
t2.micro
t3.micro
t3.medium
m5.large
c6i.large
```

Instance types determine:

* CPU
* Memory
* Network performance
* Storage performance

---

## Key Pair

Used for secure SSH access.

Consists of:

```text
Public Key
Private Key
```

AWS stores the public key.

You securely store the private key.

---

## Security Group

Acts as a virtual firewall.

Controls:

* Inbound traffic
* Outbound traffic

Example:

```text
Allow SSH (22)
Allow HTTP (80)
Allow HTTPS (443)
```

---

## EBS (Elastic Block Store)

Persistent storage attached to EC2 instances.

Data remains available even after instance stops.

---

## Region

A geographical AWS location.

Examples:

* us-east-1
* eu-west-1
* ap-south-1

---

## Availability Zone

An isolated data center within a Region.

Example:

```text
ap-south-1a
ap-south-1b
ap-south-1c
```

---

# Theoretical Understanding

## Beginner Explanation

Think of EC2 as renting a computer from AWS.

Instead of buying a laptop or server:

1. Select operating system
2. Choose hardware size
3. Launch server
4. Connect remotely
5. Pay only while using it

---

## Intermediate Explanation

EC2 provides virtualized compute resources running on AWS-managed physical infrastructure.

Users select:

* Operating system
* CPU
* Memory
* Storage
* Networking

AWS provisions a virtual machine and provides management APIs for administration.

---

## Production-Level Explanation

In enterprise environments, EC2 serves as the compute foundation for workloads including:

* Web applications
* APIs
* Databases
* CI/CD systems
* Container platforms

EC2 instances are commonly integrated with:

* VPC
* Load Balancers
* Auto Scaling Groups
* CloudWatch
* IAM
* Route 53
* Systems Manager

Production deployments emphasize:

* High Availability
* Scalability
* Security
* Monitoring
* Automation

---

# Architecture Understanding

## Components

```text
User
 │
 ▼
AWS Console / AWS CLI
 │
 ▼
EC2 Service
 │
 ├── AMI
 ├── Instance Type
 ├── Security Group
 ├── Key Pair
 └── EBS Volume
        │
        ▼
   Running EC2 Instance
```

---

## Traffic Flow

```text
Internet
   │
   ▼
Public IP
   │
   ▼
Security Group
   │
   ▼
EC2 Instance
   │
   ▼
Application
```

---

## Security Flow

```text
User
 │
 ▼
IAM Authentication
 │
 ▼
EC2 API
 │
 ▼
Security Group
 │
 ▼
Operating System
```

---

# AWS Console Walkthrough

## Objective

Launch a basic Ubuntu EC2 instance.

---

## Service Used

EC2

---

## Steps

1. Open AWS Console
2. Navigate to EC2
3. Click Launch Instance
4. Enter instance name
5. Select Ubuntu AMI
6. Choose t2.micro or t3.micro
7. Create key pair
8. Configure security group
9. Launch instance

---

## Configuration Decisions

### Ubuntu AMI

Selected because:

* Widely used
* Beginner friendly
* Extensive documentation

### t2.micro

Selected because:

* Eligible for Free Tier
* Suitable for learning

### Security Group

Allow:

```text
SSH (22)
HTTP (80)
HTTPS (443)
```

Only when required.

---

# AWS CLI Practice

## Objective

View available EC2 instances.

---

## Command

```bash
aws ec2 describe-instances
```

---

## Command Breakdown

```text
aws
 └── AWS CLI

ec2
 └── EC2 Service

describe-instances
 └── Retrieves EC2 instance information
```

---

## Expected Output

Returns:

* Instance ID
* State
* Instance Type
* Public IP
* Private IP

---

## Verification

```bash
aws ec2 describe-instances \
--query "Reservations[*].Instances[*].[InstanceId,State.Name]"
```

---

## Cleanup

No cleanup required because no resources are created.

---

# Execution Process

## Initial State

No EC2 instances running.

---

## Resource Creation

Launch EC2 instance.

---

## Configuration

Assign:

* AMI
* Security Group
* Key Pair

---

## Testing

Connect through SSH.

---

## Validation

Verify:

```bash
hostname
whoami
ip a
```

---

## Cleanup

Terminate instance after testing.

---

# Hands-On Lab

## Lab Goal

Launch and inspect an EC2 instance.

---

## Prerequisites

* AWS Account
* IAM User
* AWS CLI Installed

---

## Steps Performed

1. Open EC2 Console
2. Launch Ubuntu instance
3. Create key pair
4. Configure security group
5. Start instance

---

## Commands Executed

```bash
aws ec2 describe-instances

aws ec2 describe-regions

aws ec2 describe-availability-zones
```

---

## Validation

Verify:

```bash
aws ec2 describe-instances
```

Instance should appear in output.

---

## Result

Successfully explored EC2 fundamentals and instance deployment workflow.

---

# Observations

* EC2 instances can be provisioned within minutes.
* AWS manages physical infrastructure.
* Security Groups are stateful.
* EC2 integrates closely with networking and storage services.
* Multiple instance types support different workloads.
* Instances can be started, stopped, and terminated as needed.

---

# What I Learned

### Technical Learnings

* EC2 provides virtual servers in AWS.
* Instances are launched from AMIs.
* Security Groups act as firewalls.
* EBS provides persistent storage.

### Operational Learnings

* Instance sizing impacts cost and performance.
* Security should be configured before deployment.
* Proper key management is essential.

### Best Practices

* Use least-privilege security rules.
* Avoid opening SSH to the entire internet.
* Tag resources appropriately.
* Terminate unused resources.

---

# Troubleshooting

## Problem

Unable to SSH into EC2.

---

## Symptoms

```text
Connection timed out
```

---

## Root Cause

Possible causes:

* Port 22 blocked
* Wrong key pair
* Instance not running

---

## Investigation Commands

```bash
aws ec2 describe-security-groups

aws ec2 describe-instances
```

---

## Resolution

* Allow port 22
* Verify correct key pair
* Confirm instance state is running

---

## Verification

```bash
ssh -i key.pem ubuntu@public-ip
```

Connection successful.

---

# Real-World Relevance

Organizations use EC2 for:

* Enterprise applications
* SaaS platforms
* Development environments
* CI/CD systems
* Database servers
* Microservices

Teams interacting with EC2:

* Cloud Engineers
* DevOps Engineers
* SRE Teams
* Platform Engineers
* Security Teams

---

# Interview Preparation

## Frequently Asked Questions

### What is EC2?

EC2 is AWS's virtual machine service that provides scalable compute resources in the cloud.

---

### What is an AMI?

An AMI is a template used to launch EC2 instances.

---

### What is the difference between an AMI and an Instance?

AMI is the template.

Instance is the running virtual machine created from that template.

---

### What is a Security Group?

A stateful virtual firewall controlling instance traffic.

---

## Scenario-Based Question

Your application receives a sudden traffic spike. How can EC2 help?

### Answer

EC2 can scale horizontally by launching additional instances, typically through Auto Scaling Groups and Load Balancers.

---

# Key Takeaways

* EC2 is AWS's primary compute service.
* Instances are launched from AMIs.
* Security Groups protect instances.
* EBS provides persistent storage.
* EC2 forms the foundation for many AWS architectures.

# Skills Demonstrated

* AWS Console Operations
* AWS CLI Usage
* Cloud Infrastructure Understanding
* Compute Resource Management
* Security Fundamentals
* Basic Troubleshooting
