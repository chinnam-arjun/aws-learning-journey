# Working with Security Groups

## Objective

Understand how Security Groups control network access to EC2 instances and practice configuring inbound and outbound rules.

---

## Services Used

* Amazon EC2
* Security Groups
* AWS CLI

---

## Concepts Learned

* Security Groups act as virtual firewalls for EC2 instances.
* They are stateful, meaning return traffic is automatically allowed.
* Rules can allow traffic based on protocol, port, and source.
* Multiple instances can share the same Security Group.

---

## What I Explored

### Inbound Rules

Configured access for:

| Protocol | Port | Purpose               |
| -------- | ---- | --------------------- |
| SSH      | 22   | Remote administration |
| HTTP     | 80   | Web traffic           |
| HTTPS    | 443  | Secure web traffic    |

### Outbound Rules

Observed that outbound traffic is allowed by default.

---

## AWS CLI Commands Practiced

### List Security Groups

```bash
aws ec2 describe-security-groups
```

### View Specific Security Group

```bash
aws ec2 describe-security-groups \
--group-ids sg-xxxxxxxx
```

### Create Security Group

```bash
aws ec2 create-security-group \
--group-name ec2-lab-sg \
--description "Security group for EC2 labs"
```

### Allow SSH Access

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 22 \
--cidr 0.0.0.0/0
```

### Allow HTTP Access

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 80 \
--cidr 0.0.0.0/0
```

---

## Validation

Verified:

* SSH access to EC2 instance
* Security Group attached to instance
* Inbound rules reflected correctly
* Traffic allowed only on configured ports

---

## Problem Encountered

### Problem

SSH connection timed out.

### Investigation

Checked:

```bash
aws ec2 describe-security-groups
```

Observed that port 22 was not allowed.

### Resolution

Added SSH inbound rule.

Connection succeeded after updating the Security Group.

---

## Observations

* Security Groups deny traffic unless explicitly allowed.
* Changes take effect immediately.
* No instance reboot is required after rule changes.
* Security Groups are stateful.
* One Security Group can be attached to multiple instances.

---

## What I Learned

* Security Groups are the first place to check during connectivity issues.
* Inbound rules control who can reach the instance.
* Outbound rules control what the instance can access.
* Allowing `0.0.0.0/0` for SSH is convenient for labs but not recommended for production.
* Restricting SSH to known IP addresses improves security.

---

## Screenshots

Add screenshots for:

* Security Group Configuration
* Inbound Rules
* EC2 Instance Association
* Successful SSH Connection

---

## Architecture Notes

```text
Internet
    │
    ▼
Security Group
    │
    ├── Allow TCP 22 (SSH)
    ├── Allow TCP 80 (HTTP)
    └── Allow TCP 443 (HTTPS)
    │
    ▼
EC2 Instance
```

---

## Key Takeaway

During EC2 administration, Security Groups are one of the most common causes of connectivity issues. Understanding how they filter traffic is essential for troubleshooting and securing cloud workloads.

---

## Next Steps

* Explore Key Pairs and SSH authentication
* Connect to EC2 using SSH
* Compare Security Groups and NACLs
* Deploy a web server and test HTTP access
