---
title : "Giới thiệu"
date :  "2024-12-05"
weight : 1
chapter : false
pre : "<b>1.</b>"
---

# QUẢN LÝ HYBRID DNS VỚI ROUTE 53  
## TÍCH HỢP DNS GIỮA AWS VÀ HẠ TẦNG NỘI BỘ

---

### Tại sao cần Hybrid DNS?

Trong xu hướng chuyển đổi số hiện nay, nhiều doanh nghiệp áp dụng mô hình **hạ tầng lai (hybrid infrastructure)** — kết hợp giữa hệ thống tại chỗ (on-premises) và dịch vụ cloud như AWS. Vấn đề lớn trong mô hình này là **việc phân giải tên miền (DNS)** giữa hai môi trường.

Hệ thống DNS truyền thống thường không đủ linh hoạt và bảo mật để xử lý các truy vấn từ nhiều nguồn, dẫn đến lỗi phân giải tên, độ trễ cao hoặc mất kết nối.

---

### Mục tiêu của tài liệu này

Tài liệu hướng dẫn từng bước để xây dựng kiến trúc DNS kết hợp giữa AWS và on-prem, tập trung vào:

- Thiết lập **phân giải tên 2 chiều** giữa on-prem và AWS
- Cấu hình **split-horizon DNS** để tách biệt vùng nội bộ và vùng công khai
- Tạo **luật forward theo điều kiện** để quản lý chính xác vùng tên miền
- Kết nối hệ thống giám sát và phát hiện mối đe dọa DNS
- Hỗ trợ **khả năng khôi phục thảm họa (Disaster Recovery)** qua kiểm tra tình trạng DNS

---

### Thành phần kiến trúc chính

- **Inbound Resolver Endpoint** – Cho phép DNS on-prem truy vấn các tên miền AWS  
- **Outbound Resolver Endpoint** – Cho phép tài nguyên AWS truy vấn DNS nội bộ  
- **Private & Public Hosted Zones** – Phân tách truy vấn nội bộ và công khai  
- **Conditional Forwarding Rules** – Điều hướng theo hậu tố tên miền  
- **CloudWatch Logs** – Ghi log và phân tích truy vấn DNS  
- **GuardDuty DNS Protection** – Phát hiện truy vấn đáng ngờ

---

### Lợi ích thực tế

- Kết nối phân giải tên liền mạch giữa các môi trường  
- Nâng cao bảo mật và phát hiện bất thường qua DNS  
- Tối ưu tốc độ truy vấn bằng định tuyến hợp lý  
- Sẵn sàng khôi phục khi gặp sự cố với health checks  
- Có hướng dẫn vận hành, kiểm thử và xử lý sự cố rõ ràng

---

### Nội dung tài liệu

Bạn sẽ được hướng dẫn từng bước để thiết lập mạng, cấu hình Route 53, kết nối với hệ thống DNS nội bộ, và xác minh toàn bộ quy trình. Sau khi hoàn thành, bạn sẽ có một mô hình DNS kết hợp ổn định và bảo mật cao.

