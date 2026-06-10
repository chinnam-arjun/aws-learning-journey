# Launching My First EC2 Instance

## Objective

Launch an Ubuntu EC2 instance, configure basic access, and connect to it using SSH.

---

## Services Used

* Amazon EC2
* Security Groups
* Key Pairs

---

## Concepts Learned

* EC2 provides virtual servers in AWS.
* An AMI acts as a template for launching instances.
* Instance types determine CPU and memory resources.
* Security Groups control inbound and outbound traffic.
* Key Pairs are used for secure SSH access.

---

---

## Configuration Used

| Setting          | Value               |
| ---------------- | ------------------- |
| Operating System | Ubuntu Server       |
| Instance Type    | t2.micro / t3.micro |
| Authentication   | Key Pair            |
| Network Access   | Security Group      |
| SSH Port         | 22                  |

---

## AWS CLI Commands Practiced

### View Running Instances

```bash
aws ec2 describe-instances
```

### Show Instance IDs and State

```bash
aws ec2 describe-instances \
--query "Reservations[*].Instances[*].[InstanceId,State.Name]" \
--output table
```

### List Available Regions

```bash
aws ec2 describe-regions
```

### List Availability Zones

```bash
aws ec2 describe-availability-zones
```

## SSH Connection

Example command:

```bash
ssh -i my-key.pem ubuntu@<public-ip>
```

Successful login confirmed that:

* Instance was reachable
* Security Group rules were correct
* Key Pair authentication worked


## Architecture Notes

```text
User
 │
 ▼
AWS Console
 │
 ▼
EC2 Service
 │
 ├── Ubuntu AMI
 ├── Instance Type
 ├── Security Group
 └── Key Pair
        │
        ▼
   Running EC2 Instance
```

---

## What I Did

- Launched Ubuntu EC2 instance
- Configured SSH access
- Created Security Group for SSH
- Connected from local machine
- Verified instance status and networking
