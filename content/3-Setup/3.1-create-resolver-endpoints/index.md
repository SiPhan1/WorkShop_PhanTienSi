---
title: "Create Route 53 Resolver Endpoints"
date: 2025-07-26
weight: 1
pre : "<b>3.1 </b>"
---

# Create Route 53 Resolver Endpoints

Route 53 Resolver Endpoints are essential for enabling DNS query forwarding between AWS and on-premises environments.

---

### Inbound vs Outbound Endpoints

**Inbound Endpoint**: To enable your on-premise DNS system to query Route 53 Resolver for specific DNS zones (such as Private Zones) hosted on Route 53, you need to set up a Route 53 Inbound Endpoint. This Inbound Endpoint serves as a link for other services to request domain name resolution from Route 53. When you create an Inbound Endpoint, AWS generates an elastic network interface (ENI) in each specified availability zone (AZ) to handle incoming DNS queries.  
![inbound53](/images/prerequisite/inbound53.png)

**Outbound Endpoint**: To enable the Route 53 Resolver to forward DNS queries for domains hosted outside of Route 53. When you create a Route 53 Outbound Endpoint, AWS will generate an elastic network interface (ENI) in each specified Availability Zone (AZ).  
![outbound53](/images/prerequisite/outbound53.png)

---

### Steps to Create Endpoints

#### 1. Open the Route 53 Resolver Console

- Navigate to: [Route 53 Resolver Console](https://console.aws.amazon.com/route53resolver)  
  ![mainroute53](/images/prerequisite/mainroute53.png)

#### 2. Create an Inbound Endpoint

- Choose **Inbound Endpoint**
- Provide:
  - Name: `inbound-resolver`
  - VPC: **HybridDNS-VPC**
  - Subnets: Choose 2 **private subnets**
  - IPs: Use auto-assigned or custom IPs
- Associate a **Security Group** that allows DNS (port 53)  
  ![setupinbound](/images/prerequisite/setupinbound.png)  
  ![ipaddress](/images/prerequisite/ipaddress.png)  
- Result  
  ![finalinbound](/images/prerequisite/finalinbound.png)

#### 3. Create an Outbound Endpoint

- Choose **Outbound Endpoint**
- Provide:
  - Name: `outbound-resolver`
  - VPC: **HybridDNS-VPC**
  - Subnets: Choose 2 **private subnets**
  - IPs: Use auto-assigned or custom IPs
- Associate the same **Security Group**  
  ![finaloutbound](/images/prerequisite/finaloutbound.png)

---

### Notes

- DNS queries will use **UDP/TCP 53**
- Make sure your **on-prem firewall** allows traffic from these resolver IPs
- If EC2 can’t access external DNS, check the NACL or security group
- Store the IPs of your endpoints for use in conditional forwarding (step 3.2)
