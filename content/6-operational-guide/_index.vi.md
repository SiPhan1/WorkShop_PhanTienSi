---
title : "Vận hành hệ thống"
date :  "2024-12-05"
weight : 6
chapter : false
pre : "<b>6.</b>"
---

# Vận hành hệ thống DNS Hybrid

Phần này hướng dẫn cách vận hành, giám sát, bảo trì và kiểm soát truy cập cho hệ thống DNS Hybrid trong môi trường thực tế.

---

## Vận hành hàng ngày

- Theo dõi log truy vấn DNS thông qua **CloudWatch Logs**
- Kiểm tra trạng thái các **Health Check** trong **Route 53**
- Phân tích các bất thường trong truy vấn DNS (ví dụ: lỗi phân giải, truy vấn lặp)
- Dọn dẹp các **bản ghi DNS** hoặc **hosted zone** không còn sử dụng

---

## Quản lý truy cập (IAM)

Áp dụng nguyên tắc **least privilege** cho người quản trị DNS.

### Gợi ý chính sách IAM cho quản trị DNS:

```json
{
  "Effect": "Allow",
  "Action": [
    "route53:ChangeResourceRecordSets",
    "route53:GetHostedZone",
    "route53:ListHostedZones"
  ],
  "Resource": "*"
}
