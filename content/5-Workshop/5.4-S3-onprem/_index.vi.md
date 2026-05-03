---
title : "Phát triển REST API với Django"
date : 2026-05-01
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---



### Tổng quan

Phần này hướng dẫn xây dựng toàn bộ API backend cho website nghe nhạc bằng Django và Django REST Framework. Hệ thống API được chia thành hai nhóm chính:

- **API phía client** – phục vụ giao diện người dùng: lấy danh sách bài hát, album, nghệ sĩ, tìm kiếm, đăng ký/đăng nhập bằng JWT, quản lý playlist cá nhân.
- **API quản trị** – phục vụ giao diện admin: thêm, sửa, xóa bài hát, MV, album, nghệ sĩ, người dùng; cung cấp thống kê cho dashboard.

Backend được triển khai trên nền tảng Django 4.x, sử dụng SQLite trong quá trình phát triển (có thể chuyển sang PostgreSQL khi triển khai thật) và bảo mật bằng JWT.

#### Nội dung

1. [Xây dựng API cho client](5.4.1-client-api/) – Model, Serializer, View, Endpoint cho người dùng cuối.
2. [Xây dựng API cho admin](5.4.2-admin-api/) – Endpoint CRUD tài nguyên và thống kê dashboard.

Sau khi hoàn thành cả hai phần, bạn sẽ có một backend sẵn sàng phục vụ dữ liệu cho toàn bộ giao diện React đã xây dựng trước đó.