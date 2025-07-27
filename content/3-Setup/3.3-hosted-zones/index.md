---
title: "Set Up Hosted Zones"
date: 2025-07-26
weight: 3
pre : "<b>3.3 </b>"
---

# Set Up Public & Private Hosted Zones

Hosted Zones in Route 53 are containers for DNS records. In a hybrid setup, you may use both **public** and **private** hosted zones depending on the use case.

---

### Private Hosted Zones (PHZ)

- Used for internal domain resolution within VPC.
- Not accessible from the internet.
- Example: `internal.example.com`

#### Steps:

1. Go to [Route 53 Console](https://console.aws.amazon.com/route53/)
2. Click **Create hosted zone**
3. Domain name: `internal.example.com`
4. Type: **Private Hosted Zone**
5. Associate with `HybridDNS-VPC`

---

### Public Hosted Zones (Optional)

- Used for internet-facing services.
- Example: `hybriddns.example.com`

Steps are similar to private zones, just select **Public Hosted Zone**.

---

### Example Record Set (Private)

| Record Type | Name             | Value       |
|-------------|------------------|-------------|
| A           | `test.internal`  | `10.0.1.5`   |

---

### Screenshot About Hosted Private Zone

![Hosted Zone Example](/images/setup/hosted-zones.png)

---

### Notes

- Records in Private Zones only resolve inside the associated VPC.
- Ensure that the VPC has DNS resolution and hostnames enabled.
