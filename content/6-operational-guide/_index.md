---
title : "Operating the DNS Hybrid System"
date :  "2024-12-05"
weight : 6
chapter : false
pre : "<b>6.</b>"
---

# Operating the DNS Hybrid System

This section provides guidelines for daily operations, monitoring, maintenance, access control, and backup practices for managing the hybrid DNS setup.

---

## Daily Operations

- Monitor DNS query logs via **CloudWatch Logs**
- Check **Route 53 Health Checks** regularly
- Investigate unusual DNS behavior (e.g., failed queries, repetitive lookups)
- Clean up unused **DNS records** or **hosted zones** periodically

---

## Access Control (IAM)

Follow the **principle of least privilege** for DNS administrators.

### Suggested IAM Policy for DNS Management

```json
{
  "Effect": "Allow",
  "Action": [
    "route53:ChangeResourceRecordSets",
    "route53:GetHostedZone",
    "route53:ListHostedZones"
  ],
  "Resource": "*"
}
