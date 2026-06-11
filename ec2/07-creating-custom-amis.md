# Creating Custom AMIs

## Objective

Create a custom Amazon Machine Image (AMI) from a configured EC2 instance and use it to launch identical instances.

---

## Services Used

* Amazon EC2
* Amazon Machine Images (AMI)
* Amazon EBS

---

## Concepts Learned

* AMIs act as reusable server templates.
* A custom AMI captures the instance configuration at a specific point in time.
* New EC2 instances launched from the AMI inherit the same operating system, installed software, and configuration.
* AMIs simplify scaling, recovery, and environment standardization.

---

## What I Did

* Launched and configured an Ubuntu EC2 instance.
* Installed software on the server.
* Created a custom AMI from the instance.
* Launched a new EC2 instance using the AMI.
* Verified that configuration changes were preserved.

---

## Server Configuration Captured

Example setup before AMI creation:

```bash
sudo apt update
sudo apt install nginx -y
```

Created a test page:

```bash
echo "AMI Test Server" | sudo tee /var/www/html/index.html
```

Verified:

```bash
curl localhost
```

Expected output:

```text
AMI Test Server
```

---

## AWS CLI Commands Practiced

### Create AMI

```bash
aws ec2 create-image \
--instance-id i-xxxxxxxx \
--name "ubuntu-nginx-template" \
--description "Custom AMI with Nginx installed"
```

### View AMIs

```bash
aws ec2 describe-images \
--owners self
```

### Launch Instance from Custom AMI

```bash
aws ec2 run-instances \
--image-id ami-xxxxxxxx \
--instance-type t3.micro
```

### Verify Instance Details

```bash
aws ec2 describe-instances
```

---

## Validation

Verified:

* AMI creation completed successfully.
* New instance launched from the AMI.
* Nginx was already installed.
* Test webpage was available without additional configuration.

---

## Problem Encountered

### Problem

Expected application files were missing on the new instance.

### Investigation

Verified:

* Correct AMI was selected.
* AMI creation status completed successfully.
* Configuration changes were saved before creating the image.

### Resolution

Created a new AMI after confirming all application files existed on the source instance.

---

## Observations

* Creating an AMI is faster than manually configuring multiple servers.
* AMIs help maintain consistency across environments.
* AMI creation automatically includes snapshots of attached EBS volumes.
* Multiple instances can be launched from the same AMI.

---

## What I Learned

* How custom AMIs simplify infrastructure deployment.
* Relationship between AMIs and EBS snapshots.
* Benefits of immutable infrastructure patterns.
* Importance of creating golden images after validation.

---

## Real-World Usage

Common use cases:

* Standardized web servers
* Pre-configured application servers
* Auto Scaling launch templates
* Disaster recovery environments
* Development and testing environments

Example:

Instead of manually configuring 20 web servers, create one properly configured server, generate an AMI, and launch all servers from that image.

---

## Screenshots

Add screenshots for:

* Source EC2 Instance
* Create Image Action
* AMI Available State
* New Instance Launched from AMI
* Verification of Installed Software

---

## Architecture Notes

```text
Configured EC2 Instance
          │
          ▼
      Custom AMI
          │
          ▼
 ┌────────┼────────┐
 ▼        ▼        ▼
EC2-1   EC2-2   EC2-3
```

All instances inherit the same base configuration.

---

## Key Takeaway

Custom AMIs allow infrastructure to be replicated quickly and consistently. They reduce manual configuration effort and form the foundation for scalable and repeatable cloud deployments.

---

## Portfolio Value

This lab demonstrates:

* Infrastructure standardization
* Image management
* Deployment automation concepts
* Scaling preparation
* Operational efficiency

These concepts are frequently used in DevOps, Cloud Engineering, and Platform Engineering environments.

---

## Next Steps

* Explore Elastic IPs
* Compare AMIs and Snapshots
* Learn Launch Templates
* Build Auto Scaling Groups using custom AMIs
