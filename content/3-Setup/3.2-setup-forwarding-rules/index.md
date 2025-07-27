---
title: "Setup Forwarding Rules"
date: 2025-07-26
weight: 2
pre : "<b>3.2 </b>"
---

# Setup Conditional Forwarding Rules

This step configures rules that forward DNS queries from AWS to specific on-premises domains.

---

### What Are Forwarding Rules?

- **Conditional forwarding** allows Route 53 Resolver to direct queries for specific domain names to external DNS servers (e.g., your on-premises DNS).
- Example: All requests for `example.com` go to `192.168.1.10`.

---

### Create Forwarding Rules

1. Go to [Route 53 Resolver Console](https://console.aws.amazon.com/route53resolver)
2. Choose **Rules → Create rule**
3. Provide:
   - Rule type: **Forward**
   - Domain name: `example.com`
   - Target IPs: IP of your **on-prem DNS server**
   - Endpoint: Use your **outbound endpoint**

---

### Sample Rule

| Domain         | Forward to IP     | Endpoint          |
|----------------|-------------------|-------------------|
| `example.com`  | `192.168.1.10`    | `outbound-resolver` |

---

### Screenshot

![Forwarding Rules Example](/images/setup/forwarding-rules.png)

4. **Attaching a rule to a VPC**  
   - During creation or after, select **Associate VPC**  
   ![Cấu hình Rule với VPC](/images/setup/rulewithvpc.png)

   - Chosen VPC: **HybridDNS-VPC**  
   ![Cấu hình Rule với VPC](/images/setup/rulewithvpc1.png)

---

### Notes

- You can add multiple rules for different domains.
- Ensure your on-prem DNS server allows queries from AWS resolver IPs.
- Attach the correct rule to the VPC for the rule to work.
