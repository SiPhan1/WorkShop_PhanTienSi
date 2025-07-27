---
title: "Chuyển đổi dự phòng và Khôi phục thảm họa"
date: 2025-07-26
weight: 5
pre : "<b>3.5 </b>"
---

# Thiết lập Chuyển đổi Dự phòng và DR

Phần này hướng dẫn cách cấu hình tính sẵn sàng cao (High Availability) và khôi phục thảm họa (Disaster Recovery) cho DNS sử dụng Route 53.

---

## Bước 1: Tạo Health Check

1. Truy cập [Route 53 Console](https://console.aws.amazon.com/route53)
2. Chọn **Health Checks → Create Health Check**
3. Điền thông tin:

| Trường               | Giá trị đề xuất                  |
|----------------------|----------------------------------|
| Name                 | `OnPrem-DNS-HealthCheck`         |
| What to monitor      | `Endpoint`                       |
| IP address           | `192.168.1.10` (DNS on-prem)     |
| Protocol             | `TCP` hoặc `HTTP`                |
| Request interval     | `30 seconds`                     |
| Failure threshold    | `3`                              |

4. Nhấn **Create Health Check**
5. *(Tuỳ chọn)* Gắn health check này với bản ghi DNS dạng **Failover**

---

## Bước 2: Tạo bản ghi DNS dạng Failover

1. Vào **Route 53 → Hosted Zones**
2. Chọn hosted zone bạn muốn (VD: `dns.hybrid.local`)
3. Tạo **2 bản ghi loại A** có cùng tên:

### Bản ghi chính (Primary):

- Name: `dns.hybrid.local`
- Value: `192.168.1.10`
- Routing Policy: `Failover`
- Failover record type: `Primary`
- Health check: sử dụng health check đã tạo

### Bản ghi dự phòng (Secondary):

- Name: `dns.hybrid.local`
- Value: `10.0.1.5`
- Routing Policy: `Failover`
- Failover record type: `Secondary`
- Health check: nên bật

| Loại | Tên              | IP           | Routing Policy | Vai trò   | Health Check |
|------|------------------|--------------|----------------|-----------|---------------|
| A    | dns.hybrid.local | 192.168.1.10 | Failover       | Primary   | Có            |
| A    | dns.hybrid.local | 10.0.1.5     | Failover       | Secondary | Có            |

---

## Bước 3: Kiểm tra chuyển đổi

1. Tạm thời tắt hoặc ngắt mạng DNS on-prem
2. Dùng EC2 trong VPC kiểm tra:

```bash
dig dns.hybrid.local
nslookup dns.hybrid.local
