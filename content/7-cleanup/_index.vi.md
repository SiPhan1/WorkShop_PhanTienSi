---
title : "Dọn dẹp tài nguyên"
date :  "2024-12-05"
weight : 7
chapter : false
pre : "<b>7.</b>"
---

# Dọn Dẹp Tài Nguyên

Sau khi hoàn tất việc triển khai hoặc thử nghiệm hệ thống DNS lai, bạn cần dọn dẹp các tài nguyên không còn sử dụng để tránh phát sinh chi phí không cần thiết và đảm bảo bảo mật môi trường.

---

## 1. Xóa Bản Ghi DNS & Hosted Zone

- Truy cập **Route 53 → Hosted Zones**
- Chọn Hosted Zone (ví dụ: `internal.example.com`)
- Xóa tất cả **bản ghi** trừ **NS** và **SOA**
- Sau đó xóa toàn bộ **Hosted Zone**

![Cleanup Summary](/images/cleanup/xoaHotedzone.png)

---

## 2. Xóa Resolver Endpoint & Rules

- Truy cập **Route 53 → Resolver**
- Thực hiện các bước sau:
  - Xóa **Inbound Endpoint**

![Xóa Inbound](/images/cleanup/xoainbound.png)

- Xóa **địa chỉ IP tuỳ chỉnh** nếu đã gán

![Xóa IP](/images/cleanup/xoaIP.png)

- Xóa **Outbound Endpoint**

![Xóa Outbound](/images/cleanup/xoaoutbound.png)

- Xóa tất cả **Resolver Rules** và **liên kết rule**
- Xóa cấu hình **Query Logging**
  - Nếu logging còn chạy → **Stop trước**, sau đó mới xóa

![Xóa Query Logging](/images/cleanup/xoaquery.png)

---

## 3. Xóa Log & Cảnh Báo CloudWatch

- Vào **CloudWatch → Log Groups**:
  - Xóa log truy vấn resolver (ví dụ: `/aws/route53/resolver`)
- Vào **CloudWatch → Alarms**:
  - Xóa các cảnh báo tùy chỉnh liên quan đến **Health Check**

![Xóa CloudWatch Logs & Alarms](/images/cleanup/xoaCW.png)

---

## 4. Xóa EC2 & VPC

- Vào [EC2 Console](https://console.aws.amazon.com/ec2)
  - **Stop** và **Terminate** các EC2 dùng để kiểm thử DNS
  - Đảm bảo xóa cả **EBS volumes** nếu không dùng nữa

![Xóa EC2](/images/cleanup/xoaEC2.png)

- Vào **VPC Console**:
  - Xóa:
    - **VPC HybridDNS-VPC**
    - Các **subnet**

![Xóa subnet](/images/cleanup/xoaEdit.png)

    - **Route tables**

![Xóa Route Table](/images/cleanup/xoaRT.png)

    - **Internet Gateway**

![Xóa IGW](/images/cleanup/xoaIGW.png)

    - **NAT Gateway** (nếu tạo – để tiết kiệm chi phí)
    - **Security Group** không còn sử dụng

---

## 5. Xóa Vai Trò & Chính Sách IAM

- Xóa các **IAM role** và **policy** tạo riêng cho mục đích thử nghiệm
- Rà soát lại quyền truy cập Route 53 → thu hẹp nếu không cần nữa

![Xóa IAM Role](/images/cleanup/xoaRole.png)

---

## 6. Xóa Các Dịch Vụ Khác (Tuỳ chọn)

- Nếu có sử dụng:
  - **S3 bucket** để lưu log → Xóa
  - **Lambda function** cho tự động hóa → Xóa
- Truy cập **AWS Billing / Cost Explorer** để kiểm tra xem:
  - Còn dịch vụ nào đang âm thầm tiêu tốn chi phí không

---
