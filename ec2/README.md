# Amazon EC2 (Elastic Compute Cloud)

## Overview

Amazon EC2 (Elastic Compute Cloud) is AWS's virtual server service that provides scalable compute capacity in the cloud.

This section of the repository documents my hands-on exploration of EC2, including instance deployment, storage management, networking, monitoring, automation, troubleshooting, and production-level architecture concepts.

The objective is not only to understand EC2 theoretically but also to gain practical cloud engineering experience through AWS Console activities, AWS CLI automation, troubleshooting exercises, and real-world implementation scenarios.

---

# Learning Objectives

Through this EC2 journey, I aim to:

* Understand how virtual machines operate in AWS.
* Learn EC2 architecture and core concepts.
* Deploy and manage Linux servers in AWS.
* Configure networking and security for workloads.
* Manage storage using EBS and snapshots.
* Automate EC2 administration using AWS CLI.
* Monitor and troubleshoot EC2 instances.
* Explore scalability and high-availability patterns.
* Build production-style cloud infrastructure.

---

# Topics Covered

## Phase 1: EC2 Fundamentals

* EC2 Overview
* EC2 Architecture
* Instance Types
* Amazon Machine Images (AMI)
* Key Pairs
* Security Groups
* Elastic IP Addresses
* User Data Scripts
* EC2 Pricing Models
* Instance Lifecycle

---

## Phase 2: EC2 Storage

* Amazon EBS Overview
* EBS Volume Types
* Volume Attachment
* Filesystem Creation
* Mounting Volumes
* EBS Snapshots
* Snapshot Restoration
* EBS Encryption
* Instance Store

---

## Phase 3: EC2 Networking

* VPC and EC2 Relationship
* Public and Private Instances
* Elastic Network Interfaces (ENI)
* Internet Gateway
* Route Tables
* Security Groups
* Network ACLs
* Network Troubleshooting

---

## Phase 4: EC2 Operations

* Launching Instances
* Starting and Stopping Instances
* Rebooting Instances
* Terminating Instances
* Creating AMIs
* Restoring AMIs
* Modifying Instance Types
* Connecting Through SSH
* Managing EBS Attachments

---

## Phase 5: Monitoring and Management

* CloudWatch Metrics
* CloudWatch Alarms
* EC2 Status Checks
* AWS Systems Manager
* Session Manager
* Operational Monitoring

---

## Phase 6: Advanced EC2

* Launch Templates
* Auto Scaling Groups
* Application Load Balancer
* Network Load Balancer
* Target Groups
* Placement Groups
* Dedicated Hosts
* EC2 Hibernate

---

## Phase 7: Troubleshooting Scenarios

* SSH Connection Failures
* Security Group Misconfigurations
* Route Table Issues
* Instance Reachability Problems
* Failed Status Checks
* Disk Space Problems
* EBS Mount Failures
* Application Accessibility Issues

---

# Repository Structure

```text
ec2/
│
├── README.md
│
├── fundamentals/
│   ├── 01-ec2-overview.md
│   ├── 02-ec2-architecture.md
│   ├── 03-instance-types.md
│   ├── 04-ami-overview.md
│   ├── 05-key-pairs.md
│   ├── 06-security-groups.md
│   ├── 07-elastic-ip.md
│   ├── 08-user-data.md
│   ├── 09-pricing-models.md
│   └── 10-instance-lifecycle.md
│
├── storage/
│   ├── 01-ebs-overview.md
│   ├── 02-ebs-volume-types.md
│   ├── 03-volume-management.md
│   ├── 04-ebs-snapshots.md
│   ├── 05-ebs-encryption.md
│   └── 06-instance-store.md
│
├── networking/
│   ├── 01-vpc-and-ec2.md
│   ├── 02-public-vs-private.md
│   ├── 03-elastic-network-interface.md
│   ├── 04-route-tables.md
│   ├── 05-security-groups-vs-nacl.md
│   └── 06-network-troubleshooting.md
│
├── operations/
│   ├── 01-launch-instance-cli.md
│   ├── 02-instance-management.md
│   ├── 03-ami-creation.md
│   ├── 04-volume-operations.md
│   └── 05-ssh-connectivity.md
│
├── monitoring/
│   ├── 01-cloudwatch-metrics.md
│   ├── 02-cloudwatch-alarms.md
│   ├── 03-status-checks.md
│   └── 04-systems-manager.md
│
├── advanced/
│   ├── 01-launch-templates.md
│   ├── 02-auto-scaling-groups.md
│   ├── 03-load-balancers.md
│   ├── 04-target-groups.md
│   ├── 05-placement-groups.md
│   └── 06-dedicated-hosts.md
│
└── troubleshooting/
    ├── 01-ssh-failure.md
    ├── 02-ebs-mount-failure.md
    ├── 03-status-check-failure.md
    ├── 04-network-connectivity.md
    └── 05-application-not-reachable.md
```

---

# Tools and Technologies

The following tools are used throughout this repository:

* Amazon EC2
* Amazon EBS
* Amazon VPC
* AWS CLI
* AWS CloudWatch
* AWS Systems Manager
* Ubuntu Linux
* SSH
* Bash Shell
* Git
* GitHub

---

# Skills Demonstrated

This repository demonstrates practical experience in:

* Cloud Infrastructure Management
* AWS CLI Administration
* Linux Server Administration
* Networking Fundamentals
* Storage Management
* Security Configuration
* Monitoring and Alerting
* Troubleshooting Methodology
* Infrastructure Automation
* High Availability Design

---

# Documentation Standards

Each topic includes:

* Concept Overview
* Core Concepts
* Architecture Understanding
* AWS Console Walkthrough
* AWS CLI Practice
* Hands-On Lab
* Execution Process
* Observations
* Learnings
* Troubleshooting Notes
* Real-World Relevance
* Interview Preparation
* GitHub-Friendly Summary

The focus is on documenting actual engineering activities rather than creating certification-style notes.

---

# Portfolio Perspective

This repository serves as evidence of practical AWS experience and demonstrates:

* Hands-on cloud administration
* Infrastructure deployment skills
* AWS CLI proficiency
* Operational troubleshooting ability
* Cloud architecture understanding
* DevOps-oriented thinking

The goal is to showcase a progression from AWS beginner to a cloud and DevOps engineer capable of working with production-oriented AWS environments.

---

# Key Takeaways

* EC2 is the foundation of compute services in AWS.
* Understanding EC2 requires knowledge of compute, storage, networking, and security.
* AWS CLI automation is critical for efficient cloud operations.
* Real-world cloud engineering involves deployment, monitoring, troubleshooting, and optimization.
* Hands-on practice provides deeper understanding than theory alone.
