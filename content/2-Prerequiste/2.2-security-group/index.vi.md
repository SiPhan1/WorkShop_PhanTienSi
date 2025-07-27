---
title: "Cấu hình Security Group cho DNS"
date: 2025-07-26
weight: 2
pre : "<b>2.2 </b>"
---

# Cấu hình Security Group cho DNS

Bước này nhằm cho phép lưu lượng DNS giữa các máy EC2, các Endpoint của Route 53 Resolver và DNS server tại hệ thống on-premises.

---

## Tạo Security Group

- Tên nhóm: `DNS-SG`
- Mô tả: Cho phép truy vấn DNS (UDP/TCP 53)
- VPC: **HybridDNS-VPC**

![](/images/prerequisite/securitygroup.png)

---

## Quy tắc Inbound

| Loại             | Giao thức | Cổng | Nguồn        |
|------------------|-----------|------|--------------|
| Custom UDP Rule  | UDP       | 53   | 10.0.0.0/16  |
| Custom TCP Rule  | TCP       | 53   | 10.0.0.0/16  |

![](/images/prerequisite/inbound.png)

---

## Quy tắc Outbound

| Loại       | Giao thức | Cổng | Đích         |
|------------|-----------|------|--------------|
| All Traffic| Tất cả    | Tất cả | 0.0.0.0/0  |

![](/images/prerequisite/outbound.png)

---

## Gán Security Group cho EC2 kiểm thử

- Truy cập lại EC2 → Actions → Networking → Change Security Groups
- Gán thêm `DNS-SG` cho EC2 cần kiểm thử

![](/images/prerequisite/gansecuritygroup.png)  
![](/images/prerequisite/gansecuritygroup2.png)

>  Bạn có thể giới hạn CIDR source/destination chỉ trong VPC hoặc subnet nội bộ để tăng cường bảo mật.

---

## Ghi chú

- Các rule trên là thiết yếu để cho phép DNS forwarding giữa các môi trường.
- Nếu dùng custom DNS server on-prem, đảm bảo **firewall** cũng mở cổng TCP/UDP 53.
