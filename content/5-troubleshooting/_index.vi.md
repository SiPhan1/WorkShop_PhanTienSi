---
title : "Khắc phục sự cố"
date :  "2024-12-05"
weight : 5
chapter : false
pre : "<b>5.</b>"
---

# Khắc phục sự cố DNS trong mô hình Hybrid

Phần này trình bày các sự cố DNS thường gặp trong môi trường lai (hybrid) và cách xử lý hiệu quả, bao gồm lỗi phân giải tên miền, kết nối on-prem và giám sát qua Health Check.

---

## Các lỗi thường gặp và cách xử lý

### 1. EC2 không phân giải được tên miền

**Hiện tượng:**  
Truy vấn DNS từ EC2 trả về lỗi `NXDOMAIN`, `SERVFAIL` hoặc không phản hồi.

**Nguyên nhân có thể:**
- VPC chưa bật phân giải DNS hoặc hostname.

**Cách khắc phục:**
- Vào **VPC → Actions → Modify DNS settings**.
- Bật:
  - `Enable DNS resolution`
  - `Enable DNS hostnames`

---

### 2. Không phân giải được tên miền on-premise

**Hiện tượng:**  
Từ EC2 không truy vấn được `app.internal.example.com`.

**Nguyên nhân có thể:**
- Chưa có Outbound Resolver Endpoint.
- Sai Forwarding Rule IP.
- SG/NACL chặn cổng DNS.

**Cách khắc phục:**
- Tạo đúng Outbound Resolver Endpoint ở subnet private.
- Kiểm tra Forwarding Rule trỏ đúng IP DNS on-prem.
- Mở cổng 53 TCP/UDP trong Security Group và NACL.

---

### 3. Health Check luôn báo lỗi

**Hiện tượng:**  
Health check Route 53 luôn trạng thái **Unhealthy**.

**Nguyên nhân có thể:**
- Endpoint không phản hồi.
- Sai loại kiểm tra (TCP/HTTP).

**Cách khắc phục:**
- Đảm bảo endpoint phản hồi đúng.
- Dùng **CloudWatch Logs/Metrics** để phân tích.
- Kiểm tra firewall hoặc SG có chặn hay không.

---

## Lệnh chẩn đoán

```bash
# Truy vấn domain qua resolver mặc định
dig app.internal.example.com

# Truy vấn domain qua outbound resolver cụ thể
dig app.internal.example.com @10.0.0.2

# Kiểm tra phân giải DNS công khai
nslookup google.com
