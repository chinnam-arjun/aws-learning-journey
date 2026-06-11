# Using Elastic IP Addresses

## Objective

Allocate an Elastic IP (EIP), associate it with an EC2 instance, and understand how static public IPs are used in AWS.

---

## Services Used

* Amazon EC2
* Elastic IP Addresses

---

## Concepts Learned

* Elastic IPs provide a static public IPv4 address.
* Normal EC2 public IPs can change after stop/start operations.
* Elastic IPs remain under your AWS account until released.
* Elastic IPs can be reassociated to another instance during recovery scenarios.

---

## What I Did

* Launched an EC2 instance.
* Observed the automatically assigned public IP.
* Allocated an Elastic IP.
* Associated the Elastic IP with the instance.
* Verified connectivity using the new static IP.
* Tested persistence across instance stop/start operations.

---

## AWS CLI Commands Practiced

### Allocate Elastic IP

```bash id="c9d3v8"
aws ec2 allocate-address \
--domain vpc
```

### View Elastic IPs

```bash id="e6x0k4"
aws ec2 describe-addresses
```

### Associate Elastic IP

```bash id="0w2i5m"
aws ec2 associate-address \
--instance-id i-xxxxxxxx \
--allocation-id eipalloc-xxxxxxxx
```

### Verify Association

```bash id="h8z9qf"
aws ec2 describe-addresses
```

### Disassociate Elastic IP

```bash id="g3b7uy"
aws ec2 disassociate-address \
--association-id eipassoc-xxxxxxxx
```

### Release Elastic IP

```bash id="s5t6ac"
aws ec2 release-address \
--allocation-id eipalloc-xxxxxxxx
```

---

## Validation

Verified:

* Elastic IP successfully associated with the EC2 instance.
* SSH access worked through the Elastic IP.
* Public IP remained unchanged after stop/start.
* Instance remained reachable using the same address.

---

## Experiment Performed

### Before Elastic IP

```text id="e4awjh"
Instance Public IP:
13.x.x.x
```

After stopping and starting the instance:

```text id="o6q48h"
New Public IP:
43.x.x.x
```

### After Elastic IP

```text id="fml5xq"
Elastic IP:
15.x.x.x
```

After stopping and starting:

```text id="a9xp5d"
Elastic IP:
15.x.x.x
```

The address remained unchanged.

---

## Observations

* Elastic IPs solve the problem of changing public IP addresses.
* They are useful when DNS records point directly to an EC2 instance.
* Elastic IPs can be moved between instances during failover situations.
* Unused Elastic IPs may incur charges.

---

## What I Learned

* Difference between dynamic and static public IPs.
* How Elastic IPs improve server accessibility.
* Importance of stable addressing for production workloads.
* How AWS manages public IP reassignment.

---

## Real-World Usage

Common scenarios:

### Web Servers

Applications requiring a fixed public endpoint.

### Bastion Hosts

SSH jump servers that administrators access regularly.

### Disaster Recovery

Move the Elastic IP from a failed instance to a replacement instance.

### Legacy Systems

Applications configured to communicate with a specific public IP.

---

## Screenshots

Add screenshots for:

* Elastic IP Allocation
* Elastic IP Association
* EC2 Instance Details
* SSH Connection Using Elastic IP
* Stop/Start Validation

---

## Architecture Notes

```text id="o9o4kl"
Internet
    │
    ▼
Elastic IP
    │
    ▼
EC2 Instance
```

### Failover Scenario

```text id="6jv7km"
Elastic IP
    │
    ├── EC2-A (Failure)
    │
    ▼
Reassociate
    │
    ▼
EC2-B (Replacement)
```

---

## Key Takeaway

Elastic IPs provide a stable public address that remains under your control. They simplify administration, DNS management, and recovery workflows when public-facing services require a fixed endpoint.

---

## Portfolio Value

This lab demonstrates:

* Network administration
* AWS public addressing concepts
* Disaster recovery awareness
* Operational management of cloud resources

---

## Next Steps

* Compare Elastic IPs with Load Balancers
* Explore Route 53 DNS integration
* Learn Launch Templates
* Build Auto Scaling environments
