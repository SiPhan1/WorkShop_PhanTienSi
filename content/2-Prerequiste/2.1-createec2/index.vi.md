---
title: "Tạo EC2 và VPC để kiểm thử DNS"
date: 2025-07-26
weight: 1
pre : "<b>2.1 </b>"

---

# Tạo EC2 và VPC để kiểm thử DNS

Bước đầu tiên để triển khai kiến trúc DNS lai là tạo một môi trường cơ bản trên AWS bao gồm VPC, Subnet và máy chủ EC2 để kiểm thử.

---

## Các bước thực hiện

### 1. Tạo VPC mới

- Truy cập [VPC Console](https://console.aws.amazon.com/vpc)
- Nhấn **Create VPC** → chọn **VPC only**
- Cấu hình:
  - Tên: `HybridDNS-VPC`
  - IPv4 CIDR: `10.0.0.0/16`  
    ![](/images/prerequisite/vpc.png)

---

### 2. Tạo Subnet

Tạo **2 subnet riêng tư**:

- `10.0.1.0/24` (AZ1)  
  ![](/images/prerequisite/Subnetprivate1.png)
- `10.0.2.0/24` (AZ2)  
  ![](/images/prerequisite/subnetprivate2.png)

Tạo **1 subnet công khai**:

- `10.0.0.0/24` (AZ)  
  ![](/images/prerequisite/subnetpb.png)

---

### 3. Gắn Internet Gateway

- Vào **Internet Gateways** → tạo mới và gắn với VPC  
  ![](/images/prerequisite/IGW.png)

---

### 4. Tạo Route Table

- Route table công khai: thêm route `0.0.0.0/0` qua IGW
- Gán route table này cho subnet công khai  
  ![](/images/prerequisite/Routetable.png)

---

### 5. Khởi tạo EC2 Instance

- Truy cập [EC2 Console](https://console.aws.amazon.com/ec2)
- Chọn Amazon Linux 2 (hoặc Windows nếu cần)
- Launch instance vào một trong các **subnet riêng tư**
- Tạo Key Pair: `hybird-key`  
  ![](/images/prerequisite/key.png)
- Gán **Security Group** cho phép SSH (Linux) hoặc RDP (Windows)  
  ![](/images/prerequisite/security.png)

- Đảm bảo EC2 có thể truy cập internet thông qua NAT Gateway hoặc VPC Endpoint nếu cần

---

## Kiểm thử với EC2

Sau khi EC2 được khởi tạo, bạn có thể kết nối qua **Session Manager** hoặc **Bastion Host** để thực hiện truy vấn DNS như:

```bash
nslookup amazon.com
