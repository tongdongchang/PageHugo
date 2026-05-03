---
title: "Worklog Tuần 1"
date: 2026-03-09
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---


### Mục tiêu của tuần

* Gặp gỡ, kết nối với các thành viên trong First Cloud Journey.
* Nắm được các dịch vụ AWS cơ bản và biết cách thao tác qua console lẫn CLI.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Gặp mặt và làm quen với nhóm FCJ <br> - Đọc kỹ nội quy, quy định thực tập | 09/03/2026 | 09/03/2026 |  |
| 3   | - Tìm hiểu tổng quan về AWS và các nhóm dịch vụ chính <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... | 10/03/2026 | 10/03/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Đăng ký tài khoản AWS Free Tier <br> - Khám phá AWS Management Console & AWS CLI <br> - **Thực hành:** <br>&emsp; + Tạo tài khoản AWS <br>&emsp; + Cài đặt và cấu hình AWS CLI <br>&emsp; + Sử dụng các lệnh AWS CLI cơ bản | 11/03/2026 | 11/03/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Nghiên cứu EC2 cơ bản: <br>&emsp; + Các loại instance <br>&emsp; + AMI <br>&emsp; + EBS volumes <br>&emsp; + ... <br> - Phương thức SSH đến EC2 <br> - Tìm hiểu Elastic IP | 12/03/2026 | 13/03/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Khởi tạo EC2 instance (dùng Amazon Linux 2) <br>&emsp; + Kết nối SSH vào instance <br>&emsp; + Gắn thêm EBS volume và kiểm tra | 13/03/2026 | 13/03/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được sau tuần 1

* Hiểu rõ AWS là gì, nắm vững các nhóm dịch vụ nền tảng: Compute, Storage, Networking, Database cùng một số dịch vụ liên quan.

* Đăng ký và kích hoạt thành công tài khoản AWS Free Tier.

* Thành thạo sử dụng AWS Management Console để tìm kiếm, truy cập và quản lý dịch vụ qua giao diện web.

* Cài đặt và thiết lập AWS CLI trên máy cá nhân, bao gồm:
  * Access Key ID & Secret Access Key
  * AWS Region mặc định
  * Output format (json/yaml/table)

* Sử dụng thành thạo AWS CLI cho các tác vụ cơ bản:
  * Xác minh thông tin tài khoản và cấu hình (`aws sts get-caller-identity`, `aws configure list`)
  * Liệt kê các region khả dụng
  * Xem trạng thái dịch vụ EC2
  * Tạo và quản lý key pair
  * Kiểm tra tài nguyên đang chạy

* Có thể kết hợp linh hoạt giữa Console và CLI để quản lý tài nguyên AWS một cách song song.