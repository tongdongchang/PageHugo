---
title : "Giới thiệu"
date : 2026-05-01
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

#### Giới thiệu về Kiến trúc Website Nghe nhạc

+ Hệ thống được chia thành hai khối chính: **frontend** (React) và **backend** (Django), triển khai trên các dịch vụ AWS có khả năng mở rộng, sẵn sàng cao.
+ Frontend là một Single Page Application được lưu trữ tĩnh trên **Amazon S3**, phân phối toàn cầu qua **CloudFront** và truy cập qua tên miền riêng nhờ **Route 53**.
+ Backend chạy trên máy chủ ảo **EC2**, xử lý API và xác thực người dùng thông qua **JWT**; dữ liệu được lưu trữ trong **PostgreSQL** (có thể dùng RDS khi mở rộng). Backend có thể được truy cập an toàn từ frontend qua HTTPS mà không cần đi qua Internet công cộng.

#### Tổng quan về workshop
Trong workshop này, bạn sẽ làm việc với hai môi trường chính:
+ **Môi trường Cloud (AWS)**: nơi triển khai toàn bộ hệ thống, bao gồm S3 bucket, CloudFront distribution, Route 53 hosted zone, và EC2 instance chạy Django.
+ **Môi trường Phát triển (Local)**: mô phỏng máy trạm của lập trình viên, nơi bạn viết code React và Django, chạy thử nghiệm trước khi đưa lên AWS. Một EC2 instance (trong môi trường Cloud) có thể được dùng làm máy chủ build hoặc test từ xa, kết nối qua SSH.

Để giảm thiểu chi phí, workshop tận dụng **AWS Free Tier**, chỉ sử dụng một EC2 instance t2.micro và các dịch vụ miễn phí khác. Khi lập kế hoạch cho production, AWS khuyến nghị sử dụng nhiều AZ và dịch vụ quản lý (như RDS, Elastic Beanstalk) để đảm bảo tính sẵn sàng cao.

![overview](/images/5-Workshop/5.1-Workshop-overview/flow.png)
