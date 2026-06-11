# EC2 Monitoring with CloudWatch

## Objective

Monitor EC2 instance health and performance using Amazon CloudWatch metrics and alarms.

---

## Services Used

* Amazon EC2
* Amazon CloudWatch

---

## Concepts Learned

* CloudWatch collects performance metrics from EC2 instances.
* Metrics help identify performance bottlenecks and operational issues.
* CloudWatch Alarms can notify administrators when thresholds are exceeded.
* Monitoring is essential for maintaining application availability.

---

## What I Did

* Explored EC2 monitoring metrics.
* Viewed CPU utilization trends.
* Examined network traffic metrics.
* Reviewed disk activity metrics.
* Created a CloudWatch Alarm for high CPU utilization.
* Triggered activity on the instance to observe metric changes.

---

## Metrics Explored

| Metric            | Purpose                  |
| ----------------- | ------------------------ |
| CPUUtilization    | CPU usage percentage     |
| NetworkIn         | Incoming network traffic |
| NetworkOut        | Outgoing network traffic |
| DiskReadOps       | Disk read operations     |
| DiskWriteOps      | Disk write operations    |
| StatusCheckFailed | Instance health status   |

---

## AWS CLI Commands Practiced

### View Available Metrics

```bash
aws cloudwatch list-metrics \
--namespace AWS/EC2
```

### View CPU Utilization

```bash
aws cloudwatch get-metric-statistics \
--namespace AWS/EC2 \
--metric-name CPUUtilization \
--dimensions Name=InstanceId,Value=i-xxxxxxxx \
--statistics Average \
--period 300 \
--start-time 2026-06-10T00:00:00Z \
--end-time 2026-06-11T00:00:00Z
```

### Create CPU Alarm

```bash
aws cloudwatch put-metric-alarm \
--alarm-name HighCPUAlarm \
--metric-name CPUUtilization \
--namespace AWS/EC2 \
--statistic Average \
--period 300 \
--threshold 70 \
--comparison-operator GreaterThanThreshold \
--evaluation-periods 2
```

### View Alarms

```bash
aws cloudwatch describe-alarms
```

---

## Validation

Verified:

* EC2 metrics were visible in CloudWatch.
* CPU utilization changed during workload execution.
* Alarm was successfully created.
* Alarm state changed when threshold conditions were met.

---

## Experiment Performed

Generated CPU activity:

```bash
yes > /dev/null
```

Observed:

* CPU utilization increased significantly.
* CloudWatch metrics reflected the workload.
* Alarm moved from OK to ALARM state after threshold breach.

Stopped workload:

```bash
pkill yes
```

Observed:

* CPU utilization gradually returned to normal levels.
* Alarm returned to OK state.

---

## Observations

* CloudWatch metrics are not always real-time and may have a short delay.
* CPU spikes are clearly visible in monitoring graphs.
* Monitoring helps identify performance trends before they become incidents.
* Alarms provide proactive notification capabilities.
* EC2 instances expose several useful metrics without additional agents.

---

## What I Learned

* How CloudWatch collects EC2 performance data.
* How to analyze CPU utilization trends.
* How CloudWatch Alarms support operational monitoring.
* Basic performance troubleshooting using metrics.
* Importance of monitoring production infrastructure.

---

## Real-World Scenario

A web application becomes slow during peak traffic hours.

Investigation process:

1. Review CPUUtilization metric.
2. Check NetworkIn and NetworkOut activity.
3. Review Status Checks.
4. Determine whether the instance requires scaling or optimization.

CloudWatch provides the visibility needed to diagnose these issues.

---

## Screenshots

Add screenshots for:

* EC2 Monitoring Tab
* CPU Utilization Graph
* CloudWatch Metrics Dashboard
* CloudWatch Alarm Configuration
* Alarm State Change

---

## Architecture Notes

```text
EC2 Instance
      │
      ▼
CloudWatch Metrics
      │
      ▼
CloudWatch Alarm
      │
      ▼
Alert / Notification
```

---

## Key Takeaway

Monitoring is a core operational responsibility. CloudWatch provides visibility into EC2 performance and enables proactive detection of issues through metrics and alarms.

---

## Portfolio Value

This lab demonstrates:

* Infrastructure monitoring
* Performance analysis
* AWS CLI usage
* Operational awareness
* Basic incident detection

---

## Next Steps

* Install CloudWatch Agent
* Monitor memory and disk utilization
* Create SNS notifications for alarms
* Build Auto Scaling based on CloudWatch metrics
