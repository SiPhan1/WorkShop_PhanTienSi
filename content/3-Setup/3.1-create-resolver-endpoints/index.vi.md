---
title: "Tạo Route 53 Resolver Endpoints"
date: 2025-07-26
weight: 1
pre : "<b>3.1 </b>"
---

# Tạo Route 53 Resolver Endpoints

Route 53 Resolver Endpoints là thành phần then chốt để định tuyến truy vấn DNS giữa AWS và hệ thống on-prem.

---

### Inbound và Outbound Endpoint

**Inbound Endpoint**: Để cho phép hệ thống DNS on-premise của bạn có thể truy vấn Route 53 Resolver cho bất kỳ DNS zones nào (ví dụ: Private Zones) được host trên Route 53, bạn cần tạo Route 53 Inbound Endpoint. Inbound Endpoint là cầu nối cho các dịch vụ khác truy vấn Route 53 để phân giải tên miền. Khi bạn tạo Inbound Endpoint, AWS sẽ tạo một elastic network interface (ENI) trong mỗi availability zone (AZ) mà bạn chỉ định sẽ nhận các truy vấn DNS đi vào.  
![inbound53](/images/prerequisite/inbound53.png)

**Outbound Endpoint**: Để cho phép Route 53 Resolver chuyển tiếp các truy vấn DNS đối với tên miền được đặt trên hệ thống ngoài của Route 53. Khi bạn tạo một Outbound Endpoint trong Route 53, AWS sẽ tự động tạo một Elastic Network Interface (ENI) trong mỗi Availability Zone (AZ) mà bạn chỉ định.  
![outbound53](/images/prerequisite/outbound53.png)

---

### Các bước tạo Endpoint

#### 1. Mở Route 53 Resolver Console

- Truy cập: [Route 53 Resolver Console](https://console.aws.amazon.com/route53resolver)  
  ![mainroute53](/images/prerequisite/mainroute53.png)

#### 2. Tạo Inbound Endpoint

- Chọn **Inbound Endpoint**
- Nhập thông tin:
  - Tên: `inbound-resolver`
  - VPC: **HybridDNS-VPC**
  - Subnet: chọn 2 subnet **private**
  - IP: Dùng auto hoặc IP tùy chọn
- Gán **Security Group** cho phép DNS (port 53)  
  ![setupinbound](/images/prerequisite/setupinbound.png)  
  ![ipaddress](/images/prerequisite/ipaddress.png)  
- Kết quả:  
  ![finalinbound](/images/prerequisite/finalinbound.png)

#### 3. Tạo Outbound Endpoint

- Chọn **Outbound Endpoint**
- Nhập thông tin:
  - Tên: `outbound-resolver`
  - VPC: **HybridDNS-VPC**
  - Subnet: chọn 2 subnet **private**
  - IP: Dùng auto hoặc IP tùy chọn
- Gán **Security Group** giống ở bước trên  
  ![finaloutbound](/images/prerequisite/finaloutbound.png)

---

### Lưu ý

- DNS sử dụng **UDP/TCP port 53**
- Hệ thống on-prem phải mở firewall cho IP của resolver này
- Nếu EC2 không thể truy cập DNS ngoài, hãy kiểm tra NACL hoặc security group
- Ghi lại IP để cấu hình ở bước tiếp theo (3.2)
