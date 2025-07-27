---
title: "Enable Logging and Monitoring"
date: 2025-07-26
weight: 4
pre : "<b>3.4 </b>"
---

# Enable Logging and Monitoring for DNS Activity

Logging and monitoring are essential to troubleshoot and secure DNS operations in your hybrid environment.

---

### Enable Route 53 Resolver Query Logging

1. Go to [Route 53 Resolver Console](https://console.aws.amazon.com/route53resolver)
2. Choose **Query logging → Create query logging configuration**
3. Enter:
   - Name: `LogHybrid`
   - Destination: **CloudWatch Logs**, **S3**, or **Kinesis**
4. Select the **VPC** to associate with logging

![loghybrid](/images/setup/LogHybird.png)

---

### Logging Destinations

| Destination       | Use Case                          |
|-------------------|------------------------------------|
| CloudWatch Logs   | Real-time monitoring & alerting   |
| S3                | Long-term storage & analysis      |
| Kinesis           | Real-time streaming/forwarding    |

---

### Enable CloudWatch Metrics & Alarms

1. Go to [CloudWatch Console](https://console.aws.amazon.com/cloudwatch)
2. Create **alarms** based on DNS query count, errors, or spikes
3. Example: Alarm when `NXDOMAIN` responses exceed a defined threshold

---

### Screenshot Example

![Enable Logging & Monitoring](/images/setup/logging-monitoring.png)

---

### Tips

- Use **CloudWatch Insights** to search DNS logs
- Enable **Amazon GuardDuty** to detect suspicious DNS behavior
- Tag logging resources clearly for **cost tracking**

