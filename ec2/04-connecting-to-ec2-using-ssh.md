# Connecting to EC2 Using SSH

## Objective

Establish a secure remote connection to an EC2 instance and perform basic Linux administration tasks.

---

## Services Used

* Amazon EC2
* Security Groups
* Key Pairs
* SSH

---

## Concepts Learned

* SSH (Secure Shell) provides encrypted remote access to Linux servers.
* EC2 instances use Key Pair authentication instead of passwords by default.
* The correct username depends on the AMI being used.
* Security Group rules must allow SSH traffic on port 22.

---

## What I Did

* Downloaded the EC2 Key Pair (.pem file).
* Retrieved the instance public IP address.
* Connected to the Ubuntu EC2 instance using SSH.
* Verified server access.
* Executed basic Linux commands.
* Explored server information and networking details.

---

## Commands Practiced

### Connect to Ubuntu Instance

```bash id="1m8l44"
ssh -i my-key.pem ubuntu@<public-ip>
```

### Verify Logged-In User

```bash id="h4x3ki"
whoami
```

### Check Hostname

```bash id="eqrjci"
hostname
```

### View IP Addresses

```bash id="j7x84n"
ip a
```

### View Running Processes

```bash id="5m3rnp"
ps -ef
```

### Check System Information

```bash id="mjlwmg"
uname -a
```

### Check Disk Usage

```bash id="1c6kg0"
df -h
```

---

## Validation

Verified:

* SSH connection established successfully.
* Commands executed on the remote server.
* Instance networking information accessible.
* Linux environment operational.

---

## Problem Encountered

### Problem

SSH connection failed.

### Error

```text id="6b1uxv"
Permission denied (publickey)
```

### Investigation

Checked:

* Correct PEM file
* Correct username
* Correct public IP
* Security Group rules

### Resolution

Used the correct key pair and verified the username:

```text id="t3gfh9"
Ubuntu AMI → ubuntu
Amazon Linux → ec2-user
```

Connection succeeded afterward.

---

## Observations

* SSH access is the primary administration method for Linux EC2 instances.
* Key Pair authentication is more secure than password-based login.
* Losing the private key can prevent future access.
* Public IP changes after stop/start unless an Elastic IP is used.

---

## What I Learned

* How SSH authentication works in AWS.
* The relationship between Key Pairs and EC2 access.
* Basic Linux administration from a remote server.
* Common causes of SSH connection failures.
* How to verify connectivity and troubleshoot login issues.

---

## Screenshots

Add screenshots for:

* EC2 Instance Details
* Public IP Address
* Successful SSH Login
* Linux Commands Executed

---

## Architecture Notes

```text id="zb8slz"
Local Machine
      │
      │ SSH (Port 22)
      ▼
Security Group
      │
      ▼
EC2 Instance
      │
      ▼
Ubuntu Linux Server
```

---

## Key Takeaway

Launching an EC2 instance is only the first step. The real interaction begins after connecting through SSH, where server administration, application deployment, troubleshooting, and automation tasks are performed.

---

## Next Steps

* Install and configure a web server
* Explore EBS storage
* Create additional Linux users
* Practice package management
* Learn EC2 instance lifecycle operations
