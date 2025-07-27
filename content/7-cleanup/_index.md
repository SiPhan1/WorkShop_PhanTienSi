---
title : "Clean up"
date :  "2024-12-05"
weight : 7
chapter : false
pre : "<b>7.</b>"
---

# Clean Up Resources

After completing the Hybrid DNS setup and testing, it’s essential to clean up all unused AWS resources to avoid unexpected charges and maintain a secure, tidy environment.

---

## 1. Delete DNS Records & Hosted Zones

- Go to **Route 53 → Hosted Zones**
- Select the hosted zone (e.g., `internal.example.com`)
- Delete all **record sets** except **NS** and **SOA**
- Then delete the **Hosted Zone**

![Cleanup Summary](/images/cleanup/xoaHotedzone.png)

---

## 2. Delete Resolver Endpoints & Rules

- Go to **Route 53 → Resolver**
- Delete the following:
  - **Inbound Endpoint**

![Delete Inbound](/images/cleanup/xoainbound.png)

- **Custom IP addresses** (if manually assigned)

![Delete IP](/images/cleanup/xoaIP.png)

- **Outbound Endpoint**

![Delete Outbound](/images/cleanup/xoaoutbound.png)

- All **Resolver Rules** and their **associations**
- **Query Logging Configurations**
  - If any logging is still running → **Stop first**, then delete

![Delete Query Logging](/images/cleanup/xoaquery.png)

---

## 3. Delete CloudWatch Logs & Alarms

- Go to **CloudWatch → Log Groups**:
  - Delete resolver query logs (e.g., `/aws/route53/resolver`)
- Go to **CloudWatch → Alarms**:
  - Delete any custom alarms created for **Route 53 Health Checks**

![Delete CloudWatch](/images/cleanup/xoaCW.png)

---

## 4. Terminate EC2 Instances & Remove VPC

- Go to [EC2 Console](https://console.aws.amazon.com/ec2)
  - **Stop** and **Terminate** DNS testing EC2 instances
  - Delete associated **EBS volumes** if no longer needed

![Delete EC2](/images/cleanup/xoaEC2.png)

- Go to **VPC Console**:
  - Delete:
    - The **HybridDNS-VPC**

![Delete VPC](/images/cleanup/xoaVPC.png)

    - Associated **Subnets** (Untick select subnets and save)

![Delete Subnet](/images/cleanup/xoaEdit.png)

    - **Route Tables**

![Delete Route Tables](/images/cleanup/xoaRT.png)

    - **Internet Gateway**

![Delete IGW](/images/cleanup/xoaIGW.png)

    - **NAT Gateway** (to avoid high costs)
    - Any unused **Security Groups**

---

## 5. IAM Roles & Permissions

- Remove IAM **roles** and **policies** used during testing
- Review remaining **Route 53** permissions and restrict if not needed

![Delete IAM Role](/images/cleanup/xoaRole.png)

---

## 6. Remove Other Resources (Optional)

- If used:
  - **S3 buckets** for logging → delete them
  - **Lambda functions** for automation → delete them
- Use **AWS Billing / Cost Explorer** to verify that:
  - No hidden or unused services remain active

---
