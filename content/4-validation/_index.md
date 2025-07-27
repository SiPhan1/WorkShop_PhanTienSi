---
title : "Validation"
date :  "2024-12-05"
weight : 4
chapter : false
pre : "<b>4.</b>"
---

# Validate Your Hybrid DNS Setup

This section walks you through testing your DNS resolution across AWS and on-premises to ensure everything is functioning properly.

---

## Validation Steps

### 1. Connect to EC2 Instance
- Use **Session Manager** or **SSH** to connect to the EC2 instance in the private subnet.

### 2. Test Internal Domain Resolution (Private Hosted Zone)
- Ensure the DNS server (127.0.0.1) responds to queries like `app.internal.example.com`.

![testPHZ](/images/setup/testPHZ.png)

### 3. Testing from Another EC2 (via Resolver Rule)
- Validate that conditional forwarding to on-prem DNS is functioning as configured.

![testEC2](/images/setup/testEC2.png)

### 4. Test DNS via Outbound Resolver
- Queries sent from EC2 in the private subnet:
  - Go through **Outbound Endpoint**
  - Forwarded to on-prem or target resolver
  - Must return a valid DNS response

![testoutbound](/images/setup/testoutbound.png)

```bash
dig app.internal.example.com @127.0.0.1   # (2)
nslookup google.com                       # (3)
dig app.internal.example.com @10.0.0.2    # (4)
