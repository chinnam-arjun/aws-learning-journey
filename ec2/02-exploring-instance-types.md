# Exploring EC2 Instance Types

## Objective

Understand how EC2 instance types differ in CPU, memory, networking, and workload suitability.

---

## Services Used

* Amazon EC2
* AWS CLI

---

## Concepts Learned

* Instance types define the hardware resources allocated to an EC2 instance.
* Different workloads require different CPU and memory configurations.
* Instance families are optimized for specific use cases.
* Choosing the wrong instance type can impact performance and cost.

---

## Instance Families Explored

| Family | Purpose                              |
| ------ | ------------------------------------ |
| T      | General purpose, burstable workloads |
| M      | Balanced compute and memory          |
| C      | Compute optimized                    |
| R      | Memory optimized                     |
| G      | GPU workloads                        |

---

## What I Explored

* Compared commonly used EC2 instance families.
* Examined CPU and memory differences.
* Identified suitable workloads for each family.
* Reviewed instance sizing patterns.

### Examples

| Instance Type | vCPU | Memory |
| ------------- | ---- | ------ |
| t2.micro      | 1    | 1 GiB  |
| t3.micro      | 2    | 1 GiB  |
| t3.small      | 2    | 2 GiB  |
| t3.medium     | 2    | 4 GiB  |
| m5.large      | 2    | 8 GiB  |

---

## AWS CLI Commands Practiced

### List Available Instance Types

```bash
aws ec2 describe-instance-types
```

### View Specific Instance Type

```bash
aws ec2 describe-instance-types \
--instance-types t3.micro
```

### View vCPU Information

```bash
aws ec2 describe-instance-types \
--instance-types t3.micro \
--query "InstanceTypes[*].VCpuInfo"
```

### View Memory Information

```bash
aws ec2 describe-instance-types \
--instance-types t3.micro \
--query "InstanceTypes[*].MemoryInfo"
```

---

---

## Observations

* T-family instances are commonly used for learning and small workloads.
* Instance sizes scale predictably within the same family.
* More CPU and memory generally increase cost.
* Different instance families target different application requirements.

---

## What I Learned

* Instance selection is a balance between performance and cost.
* T-family instances are suitable for development and testing environments.
* M-family instances provide balanced resources for general applications.
* Compute-intensive workloads benefit from C-family instances.
* Memory-heavy workloads benefit from R-family instances.

---

---

## Architecture Notes

```text
Application
     │
     ▼
Workload Requirements
     │
     ├── General Purpose  → T / M Family
     ├── Compute Heavy    → C Family
     ├── Memory Heavy     → R Family
     └── GPU Workloads    → G Family
```

---
