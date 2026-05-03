---
title: "Workshop"
date: 2026-05-01
weight: 5
chapter: false
pre: " <b> 4. </b> "
---



# Xây dựng và triển khai Website nghe nhạc Full‑stack trên AWS

#### Tổng quan

Workshop này hướng dẫn bạn từng bước xây dựng một **website nghe nhạc trực tuyến** hoàn chỉnh, bao gồm giao diện người dùng (React), giao diện quản trị (React), API backend (Django) và triển khai lên hạ tầng AWS sử dụng các dịch vụ S3, CloudFront, Route 53 và EC2.

Trong quá trình thực tập 8 tuần, workshop được chia thành 6 phần chính, tương ứng với từng giai đoạn của dự án. Mỗi phần bao gồm hướng dẫn chi tiết các bước thực hành để bạn có thể tự mình tái tạo lại hệ thống.

#### Nội dung

1. [Tổng quan về workshop](5.1-workshop-overview/)  
   Giới thiệu mục tiêu, kiến trúc hệ thống và các dịch vụ AWS sẽ sử dụng.

2. [Chuẩn bị môi trường và công cụ](5.2-prerequisites/)  
   Cài đặt Node.js, Python, AWS CLI, cấu hình tài khoản AWS Free Tier, tạo key pair, clone source code mẫu.

3. [Xây dựng giao diện người dùng và quản trị bằng React](5.3-frontend/)  
   - Khởi tạo dự án React với Vite, cấu trúc thư mục.  
   - Xây dựng các trang: Home, Login/Register, Album, Playlist, Music Player, Search, MV.  
   - Xây dựng giao diện Admin: quản lý bài hát, MV, nghệ sĩ, album, người dùng.

4. [Phát triển REST API với Django](5.4-backend/)  
   - Tạo dự án Django, cấu hình cơ sở dữ liệu, DRF, JWT.  
   - API phía client: bài hát, nghệ sĩ, album, playlist, tìm kiếm, xác thực.  
   - API quản trị: CRUD tất cả tài nguyên, thống kê dashboard.

5. [Triển khai ứng dụng lên AWS](5.5-deployment/)  
   - Đưa frontend lên S3, cấu hình CloudFront và Route 53.  
   - Khởi chạy EC2, cài đặt Gunicorn + Nginx, cấu hình HTTPS.  
   - Kết nối frontend và backend.

6. [Kiểm thử, giám sát và tổng kết](5.6-testing/)  
   - Kiểm thử chức năng, bảo mật, hiệu năng.  
   - Dọn dẹp tài nguyên AWS sau khi hoàn thành.

#### Lưu ý khi làm workshop

- Tận dụng **AWS Free Tier** để tránh phát sinh chi phí.
- Luôn sao lưu source code lên Git thường xuyên.
- Mỗi phần có thể thực hiện độc lập trong 1–2 buổi, phù hợp với lịch trình thực tập.

Bắt đầu với phần đầu tiên: [Tổng quan về workshop](5.1-workshop-overview/)