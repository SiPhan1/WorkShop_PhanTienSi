---
title : "Thiết lập hệ thống DNS"
date : "2024-12-06"
weight : 3
chapter : false
pre : "<b>3.</b>"
---

# CẤU HÌNH DNS RESOLVER

Phần này hướng dẫn chi tiết cách triển khai hệ thống DNS lai (Hybrid DNS) giữa AWS Route 53 và máy chủ DNS on-premises của bạn.
---

## Bạn sẽ thực hiện:
- Tạo **Route 53 Resolver Endpoints** (inbound và outbound)
- Cấu hình **Luồng chuyển tiếp DNS (Conditional Forwarding)**
- Thiết lập **Hosted Zones** (private/public)
- Bật **giám sát và ghi log truy vấn DNS**
- Triển khai phương án **khôi phục sự cố và chuyển đổi dự phòng (DR)**

Mỗi bước đều kèm ảnh minh họa, chỉ dẫn qua AWS Console và cách xác minh kết quả.
