---
title: "Cấu hình Forwarding Rules"
date: 2025-07-26
weight: 2
pre : "<b>3.2 </b>"
---


# Cấu hình chuyển tiếp DNS có điều kiện (Forwarding Rules)

Bước này giúp định tuyến các truy vấn DNS từ AWS đến các tên miền cụ thể tại hệ thống on-prem.

---

### Forwarding Rules là gì?

- **Forwarding Rules** cho phép Route 53 Resolver chuyển tiếp các truy vấn DNS đến DNS server bên ngoài (ví dụ: máy chủ DNS on-prem).
- Ví dụ: Tất cả yêu cầu tên miền `example.com` sẽ được gửi đến `192.168.1.10`.

---

### Các bước cấu hình

1. Truy cập [Route 53 Resolver Console](https://console.aws.amazon.com/route53resolver)
2. Chọn **Rules → Create rule**
3. Điền thông tin:
   - Rule type: **Forward**
   - Domain: `example.com`
   - IP đích: địa chỉ DNS server on-prem
   - Endpoint: sử dụng **Outbound Endpoint**

---

### Ví dụ

| Domain         | Chuyển đến IP    | Endpoint            |
|----------------|------------------|---------------------|
| `example.com`  | `192.168.1.10`   | `outbound-resolver` |

---

### Hình minh họa

![Cấu hình Forwarding Rules](/images/setup/forwarding-rules.png)

4. **Gắn rule vào VPC**
   - Trong bước tạo hoặc sau khi tạo rule → chọn Associate VPC  
     ![Cấu hình Rule với VPC](/images/setup/rulewithvpc.png)  
   - Chọn VPC: **HybridDNS-VPC**  
     ![Cấu hình Rule với VPC](/images/setup/rulewithvpc1.png)

---

### Ghi chú

- Có thể tạo nhiều rule cho các tên miền khác nhau.
- Đảm bảo firewall on-prem cho phép truy vấn DNS từ IP của resolver AWS.
- Gắn rule đúng với VPC để rule hoạt động.
