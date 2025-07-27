---
title: "Thiết lập Hosted Zones"
date: 2025-07-26
weight: 3
pre : "<b>3.3 </b>"
---

# Thiết lập Public & Private Hosted Zones

Hosted Zones trong Route 53 là nơi chứa các bản ghi DNS. Trong mô hình DNS lai, ta có thể sử dụng cả **Hosted Zone riêng tư (Private)** và **Hosted Zone công khai (Public)**.

---

### Hosted Zone Riêng tư (PHZ)

- Dùng để phân giải tên miền nội bộ trong VPC.
- Không truy cập được từ internet.
- Ví dụ: `internal.example.com`

#### Các bước thực hiện:

1. Truy cập [Route 53 Console](https://console.aws.amazon.com/route53/)
2. Chọn **Create hosted zone**
3. Domain name: `internal.example.com`
4. Type: **Private Hosted Zone**
5. Liên kết với VPC `HybridDNS-VPC`

---

### Hosted Zone Công khai (Tuỳ chọn)

- Dùng cho các dịch vụ hướng internet.
- Ví dụ: `hybriddns.example.com`

Tạo tương tự như Hosted Zone riêng tư, chỉ cần chọn **Public Hosted Zone**.

---

### Ví dụ bản ghi (Private)

| Loại bản ghi | Tên              | Giá trị IP   |
|--------------|------------------|--------------|
| A            | `test.internal`  | `10.0.1.5`   |

---

### Hình minh họa về Hosted Zone Riêng tư

![Minh họa Hosted Zones](/images/setup/hosted-zones.png)

---

### Ghi chú

- Bản ghi trong Private Zone chỉ phân giải được bên trong VPC.
- Kiểm tra VPC đã bật DNS resolution và DNS hostname.
