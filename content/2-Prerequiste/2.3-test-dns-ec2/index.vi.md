---
title: "Kiểm thử DNS sau cấu hình SG"
date: "2024-12-06"
weight: 3
chapter: true
pre : "<b>2.3 </b>"

---

# Kiểm thử truy vấn DNS

-  Thực hiện lại lệnh:
``nslookup amazon.com``
- Kết quả hiển thị IP tương ứng là DNS hoạt động.

![testDNS](/images/prerequisite/testDNS.png)

---

###  Cài đặt công cụ DNS

Sau khi SSH vào máy EC2, chạy lệnh sau để cài công cụ kiểm tra DNS:

```bash
sudo yum install -y bind-utils
