---
title: "DNS Testing After SG Configuration"
date: "2024-12-06"
weight: 3
chapter: true
pre : "<b>2.3 </b>"

---

# DNS Query Testing

-  Execute the order again:
``nslookup amazon.com``
- The results show that the corresponding IP is active DNS.

![testDNS](/images/prerequisite/testDNS.png)

---

###  Install Tools

SSH into the EC2 and install DNS tools:
```bash
sudo yum install -y bind-utils
