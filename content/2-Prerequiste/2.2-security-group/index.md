---
title: "Configure Security Group for DNS"
date: 2025-07-26
weight: 2
pre : "<b>2.2 </b>"
---

# Configure Security Group for DNS Traffic

This step allows DNS traffic to flow between EC2 instances, Route 53 Resolver Endpoints, and your on-premises DNS servers.

---

## Create Security Group

- Security group name: `DNS-SG`
- Description: Allow DNS queries (UDP/TCP 53)
- VPC: **HybridDNS-VPC**

![](/images/prerequisite/securitygroup.png)

---

## Inbound Rules

| Type             | Protocol | Port | Source       |
|------------------|----------|------|--------------|
| Custom UDP Rule  | UDP      | 53   | 10.0.0.0/16  |
| Custom TCP Rule  | TCP      | 53   | 10.0.0.0/16  |

![](/images/prerequisite/inbound.png)

---

## Outbound Rules

| Type        | Protocol | Port  | Destination   |
|-------------|----------|-------|----------------|
| All Traffic | All      | All   | 0.0.0.0/0      |

![](/images/prerequisite/outbound.png)

---

## Assigning the SG to an EC2 Test Instance

- Go to EC2 → Actions → Networking → Change Security Groups
- Add `DNS-SG` to the test instance

![](/images/prerequisite/gansecuritygroup.png)  
![](/images/prerequisite/gansecuritygroup2.png)

>  You can restrict the source/destination CIDRs to internal subnets or your on-prem ranges for better security.

---

## Notes

- These rules are essential to enable DNS query forwarding across environments.
- If you're using custom DNS servers on-premises, make sure firewalls allow TCP/UDP 53.
