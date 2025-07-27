---
title : "Kiểm tra hoạt động"
date :  "2024-12-05"
weight : 4
chapter : false
pre : "<b>4.</b>"
---

# Kiểm tra hệ thống DNS Hybrid

Phần này hướng dẫn cách kiểm thử hệ thống DNS lai giữa AWS và on-prem.

---

## Các bước kiểm thử

### 1. Truy cập EC2 Instance
- Dùng **Session Manager** hoặc **SSH** để vào EC2 trong subnet riêng.

### 2. Kiểm tra phân giải miền nội bộ (Private Hosted Zone)
- Kiểm tra xem DNS server chạy tại `127.0.0.1` có trả lời truy vấn `app.internal.example.com` không.

![testPHZ](/images/setup/testPHZ.png)

### 3. Kiểm tra từ EC2 khác (qua resolver rule)
- Kiểm tra quy tắc chuyển tiếp DNS (Conditional Forwarding) đến DNS on-prem.

![testEC2](/images/setup/testEC2.png)

### 4. Kiểm tra DNS ở outbound
- Truy vấn từ EC2 trong subnet riêng:
  - Qua Outbound Endpoint
  - Chuyển tiếp đến DNS on-prem hoặc đích cấu hình
  - Và nhận phản hồi

![testoutbound](/images/setup/testoutbound.png)

```bash
dig app.internal.example.com @127.0.0.1   # (2)
nslookup google.com                       # (3)
dig app.internal.example.com @10.0.0.2    # (4)
