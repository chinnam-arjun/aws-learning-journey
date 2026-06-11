# Load Balancer and Auto Scaling Lab

## Objective

Deploy multiple EC2 instances behind a Load Balancer and configure Auto Scaling to automatically adjust capacity based on demand.

---

## Services Used

* Amazon EC2
* Elastic Load Balancer (ALB)
* Target Groups
* Auto Scaling Groups
* CloudWatch

---

## Concepts Learned

* Load Balancers distribute traffic across multiple servers.
* Auto Scaling automatically adds or removes instances based on demand.
* Target Groups determine which instances receive traffic.
* CloudWatch metrics can trigger scaling actions.
* Combining these services improves availability and scalability.

---

## What I Did

* Created a simple web server template.
* Created a Target Group.
* Created an Application Load Balancer.
* Registered EC2 instances with the Target Group.
* Created a Launch Template.
* Created an Auto Scaling Group.
* Configured scaling policies using CPU utilization.
* Verified traffic distribution and automatic scaling behavior.

---

## Architecture Built

```text
Users
  │
  ▼
Application Load Balancer
  │
  ▼
Target Group
  │
  ├── EC2 Instance 1
  ├── EC2 Instance 2
  └── EC2 Instance N
          │
          ▼
   Auto Scaling Group
          │
          ▼
     CloudWatch
```

---

## AWS CLI Commands Practiced

### Create Launch Template

```bash
aws ec2 create-launch-template \
--launch-template-name web-template \
--launch-template-data file://template.json
```

### Create Target Group

```bash
aws elbv2 create-target-group \
--name web-target-group \
--protocol HTTP \
--port 80 \
--vpc-id vpc-xxxxxxxx
```

### Create Load Balancer

```bash
aws elbv2 create-load-balancer \
--name web-alb \
--subnets subnet-xxxx subnet-yyyy
```

### Create Auto Scaling Group

```bash
aws autoscaling create-auto-scaling-group \
--auto-scaling-group-name web-asg \
--launch-template LaunchTemplateName=web-template \
--min-size 2 \
--max-size 4 \
--desired-capacity 2 \
--vpc-zone-identifier subnet-xxxx,subnet-yyyy
```

### View Auto Scaling Groups

```bash
aws autoscaling describe-auto-scaling-groups
```

### View Target Health

```bash
aws elbv2 describe-target-health \
--target-group-arn <target-group-arn>
```

---

## Validation

Verified:

* Load Balancer received traffic.
* Target instances passed health checks.
* Requests were distributed across instances.
* Auto Scaling Group maintained desired capacity.
* New instances launched automatically when scaling conditions were met.

---

## Experiment Performed

### Initial State

```text
Desired Capacity: 2
Running Instances: 2
```

### Generated Load

Executed on EC2 instances:

```bash
yes > /dev/null
```

Observed:

```text
CPU Utilization Increased
CloudWatch Alarm Triggered
Scaling Policy Executed
```

### Result

```text
Desired Capacity: 3
Running Instances: 3
```

A new EC2 instance was automatically launched.

After load stopped:

```bash
pkill yes
```

Observed:

```text
CPU Utilization Dropped
Scale-In Policy Triggered
```

Capacity returned to normal.

---

## Observations

* Load Balancer continued serving traffic even when instances were added or removed.
* Auto Scaling responded automatically to increased demand.
* Health checks prevented unhealthy instances from receiving traffic.
* Scaling actions required a few minutes to complete.
* The architecture became more resilient than a single-instance deployment.

---

## What I Learned

* How traffic distribution works in AWS.
* How Auto Scaling maintains application availability.
* How CloudWatch metrics drive scaling decisions.
* Why Launch Templates are important for repeatable deployments.
* Benefits of highly available architectures.

---

## Real-World Scenario

A web application experiences a traffic spike during a product launch.

Without Auto Scaling:

* Server overload
* Slow response times
* Potential downtime

With ALB + Auto Scaling:

* New instances launch automatically
* Traffic is distributed evenly
* Application remains available

---

## Screenshots

Add screenshots for:

* Load Balancer Configuration
* Target Group Health Checks
* Auto Scaling Group
* CloudWatch Alarm
* Scaling Activity History
* Multiple Running Instances

---

## Key Takeaway

This lab demonstrates how AWS handles high availability and scalability. Instead of relying on a single server, traffic is distributed across multiple instances, and capacity automatically adjusts to demand.

---

## Portfolio Value

This is one of the strongest EC2 labs because it demonstrates:

* High Availability
* Scalability
* Load Balancing
* Monitoring
* Automation
* Production-Oriented Architecture

These are concepts commonly discussed in Cloud Engineer, DevOps Engineer, and SRE interviews.

---

## Next Steps

* Create a custom AMI for Auto Scaling deployments
* Integrate SNS notifications
* Configure Route 53 with the Load Balancer
* Build a complete highly available web application architecture
* Explore multi-AZ production deployments
