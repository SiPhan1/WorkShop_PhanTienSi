---
title: "Create EC2 & VPC"
date: 2025-07-26
weight: 1
pre : "<b>2.1 </b>"
---

# Create EC2 and VPC for Hybrid DNS Testing

To begin setting up a Hybrid DNS architecture, we start by creating a foundational AWS environment including VPC, subnets, and an EC2 instance for testing DNS resolution.

---

## Steps to Follow

### 1. Create a New VPC

- Go to [VPC Console](https://console.aws.amazon.com/vpc)
- Click **Create VPC** → choose **VPC only**
- Provide:
  - Name: `HybridDNS-VPC`
  - IPv4 CIDR block: `10.0.0.0/16`  
  ![](/images/prerequisite/vpc.png)

---

### 2. Create Subnets

Create **2 private subnets**:

- `10.0.1.0/24` (AZ1)  
  ![](/images/prerequisite/Subnetprivate1.png)
- `10.0.2.0/24` (AZ2)  
  ![](/images/prerequisite/subnetprivate2.png)

Create **1 public subnet**:

- `10.0.0.0/24` (AZ)  
  ![](/images/prerequisite/subnetpb.png)

---

### 3. Create and Attach Internet Gateway

- Go to **Internet Gateways**, create a new one
- Attach it to the VPC  
  ![](/images/prerequisite/IGW.png)

---

### 4. Create Route Tables

- Create a **public route table**
  - Add route: `0.0.0.0/0` via the Internet Gateway
  - Associate it with the public subnet  
    ![](/images/prerequisite/Routetable.png)

---

### 5. Launch EC2 Instance

- Navigate to [EC2 Console](https://console.aws.amazon.com/ec2)
- Choose Amazon Linux 2 or Windows Server (optional)
- Launch the instance in a **private subnet**
- Create a key pair: `hybird-key`  
  ![](/images/prerequisite/key.png)
- Attach a **Security Group** allowing:
  - SSH (for Linux) or RDP (for Windows)  
  ![](/images/prerequisite/security.png)
- Ensure internet access via NAT Gateway or VPC Endpoints if required

---

## EC2 Testing

Once launched, connect via **Session Manager** or **Bastion Host**.

Use the EC2 instance to run DNS queries like:

```bash
nslookup amazon.com
