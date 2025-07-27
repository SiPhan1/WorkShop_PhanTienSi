---
title : "Giới thiệu"
date :  "2024-12-05"
weight : 1
chapter : false
pre : "<b>1.</b>"
---

# QUẢN LÝ HYBRID DNS VỚI ROUTE 53  
## TÍCH HỢP HỆ THỐNG DNS AWS VÀ DNS NỘI BỘ (ON-PREMISES)

---

### Tổng quan

Tài liệu này cung cấp hướng dẫn toàn diện về cách xây dựng, triển khai và quản lý kiến trúc **Hybrid DNS** kết hợp giữa hệ thống DNS nội bộ và dịch vụ **Route 53 Resolver** của AWS.

Giải pháp bao gồm các tính năng như: **conditional forwarding**, **split-horizon DNS**, **giám sát qua CloudWatch**, và **hỗ trợ khôi phục thảm họa (DR)**.

---

### Tính năng chính

- **Phân giải DNS hai chiều** giữa AWS và hệ thống nội bộ
- **Forward có điều kiện** theo tên miền cụ thể
- **Split-horizon DNS** với cả public & private hosted zone
- **Giám sát DNS** bằng CloudWatch, log truy vấn
- **Tích hợp GuardDuty** phát hiện bất thường DNS
- **Hướng dẫn vận hành** & **runbook xử lý sự cố**
- **Khôi phục thảm họa** với health check và failover Route 53

---

### Cấu trúc nội dung

1. [Giới thiệu](../1-Introduce/)
2. [Chuẩn bị](../2-Prerequisite/)
3. [Cài đặt Resolver và Split-DNS](../3-Setup/)
4. [Kiểm tra & Xác minh](../4-validation/)
5. [Xử lý sự cố](../5-troubleshooting/)
6. [Hướng dẫn vận hành](../6-operational-guide/)
7. [Xóa tài nguyên](../7-cleanup/)

---

### Sơ đồ kiến trúc hệ thống

![Sơ đồ Hybrid DNS Architecture](/images/Dns-architecture.png)
