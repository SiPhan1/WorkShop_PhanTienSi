---
title: "Bật Logging và Monitoring"
date: 2025-07-26
weight: 4
pre : "<b>3.4 </b>"
---

# Bật ghi log và giám sát truy vấn DNS

Việc ghi log và giám sát là cần thiết để theo dõi, xử lý sự cố và bảo mật hệ thống DNS trong kiến trúc hybrid.

---

### Bật ghi log truy vấn DNS trong Route 53

1. Truy cập [Route 53 Resolver Console](https://console.aws.amazon.com/route53resolver)
2. Chọn **Query logging → Create query logging configuration**
3. Nhập:
   - Tên: `LogHybrid`
   - Đích ghi log: **CloudWatch Logs**, **S3**, hoặc **Kinesis**
4. Chọn **VPC** cần ghi log

![loghybrid](/images/setup/LogHybird.png)

---

### Các đích ghi log

| Đích ghi log       | Trường hợp sử dụng                   |
|--------------------|--------------------------------------|
| CloudWatch Logs    | Giám sát và cảnh báo thời gian thực |
| S3                 | Lưu trữ lâu dài, phân tích dữ liệu   |
| Kinesis            | Stream dữ liệu thời gian thực        |

---

### Bật CloudWatch Metrics & Alarms

1. Truy cập [CloudWatch Console](https://console.aws.amazon.com/cloudwatch)
2. Tạo **alarm** dựa trên các chỉ số DNS
3. Ví dụ: cảnh báo khi số phản hồi `NXDOMAIN` vượt ngưỡng

---

### Hình minh họa

![Bật log và giám sát DNS](/images/setup/logging-monitoring.png)

---

### Mẹo

- Dùng **CloudWatch Insights** để tìm log DNS nhanh
- Tích hợp **GuardDuty** để phát hiện hoạt động DNS đáng ngờ
- **Tag tài nguyên rõ ràng** để dễ quản lý chi phí
