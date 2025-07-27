---
title: "Failover and Disaster Recovery Setup"
date: 2025-07-26
weight: 5
pre : "<b>3.5 </b>"
---

# Configuring Failover and Disaster Recovery (DR)

This section walks you through setting up High Availability (HA) and Disaster Recovery (DR) for your hybrid DNS setup using AWS Route 53.

---

## Step 1: Configure Health Check in Route 53

1. Go to [Route 53 Console](https://console.aws.amazon.com/route53)
2. Select **Health Checks → Create Health Check**
3. Use the following values:

| Field             | Recommended Value                              |
|------------------|--------------------------------------------------|
| Name              | `OnPrem-DNS-HealthCheck`                        |
| What to monitor   | `Endpoint`                                      |
| IP address        | `192.168.1.10` *(on-prem DNS IP)*              |
| Protocol          | `TCP` or `HTTP` *(depends on DNS service)*     |
| Request interval  | `30 seconds` *(default)*                        |
| Failure threshold | `3` *(after 3 failures, considered unhealthy)*  |

4. Click **Create Health Check**
5. *(Optional)*: Link it to a **failover** DNS record in the next step

---

## Step 2: Enable DNS Failover Records

1. Go to **Route 53 → Hosted Zones**
2. Choose the hosted zone (e.g., `dns.hybrid.local`)
3. Create **two A records** with the same name:

### Primary Record:
- Name: `dns.hybrid.local`
- Value: `192.168.1.10`
- Routing Policy: `Failover`
- Failover type: `Primary`
- Health Check: the one created in Step 1

### Secondary Record:
- Name: `dns.hybrid.local`
- Value: `10.0.1.5`
- Routing Policy: `Failover`
- Failover type: `Secondary`
- Health Check: optional but recommended

| Type | Name              | IP Address    | Routing Policy | Role      | Health Check |
|------|-------------------|---------------|----------------|-----------|---------------|
| A    | dns.hybrid.local  | 192.168.1.10  | Failover       | Primary   | Yes           |
| A    | dns.hybrid.local  | 10.0.1.5      | Failover       | Secondary | Yes           |

---

## Step 3: Test the Failover

1. Simulate failure by stopping or disconnecting the on-prem DNS
2. From an EC2 instance or VPC client, test:

```bash
dig dns.hybrid.local
nslookup dns.hybrid.local
