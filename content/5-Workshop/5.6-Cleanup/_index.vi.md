---
title : "Kiểm thử, giám sát và tổng kết"
date : 2026-05-01
weight : 6
chapter : false
pre : " <b> 4.6. </b> "
---

### Mục tiêu

Sau khi đã triển khai thành công website nghe nhạc lên AWS, chúng ta cần đảm bảo hệ thống hoạt động đúng đắn, an toàn và có hiệu năng ở mức chấp nhận được. Phần này sẽ hướng dẫn bạn:

- Kiểm thử chức năng toàn bộ luồng người dùng và quản trị.
- Đánh giá các khía cạnh bảo mật cơ bản.
- Đo lường hiệu năng sơ bộ.
- Dọn dẹp tài nguyên AWS để tránh phát sinh chi phí sau khi hoàn tất.

---

#### 1. Kiểm thử chức năng

##### 1.1. Phía người dùng (client)

Mở trình duyệt và truy cập địa chỉ S3 static website (hoặc CloudFront nếu đã cấu hình). Thực hiện lần lượt các thao tác:

| # | Tác vụ | Kết quả mong đợi |
|---|--------|------------------|
| 1 | Truy cập trang chủ | Hiển thị banner, danh sách bài hát gợi ý, nghệ sĩ, album. Không có lỗi console. |
| 2 | Đăng ký tài khoản mới | Form `username`, `email`, `password`, `confirmPassword`. Đăng ký thành công, chuyển sang trang đăng nhập. |
| 3 | Đăng nhập | Sau khi đăng nhập, header hiển thị avatar/username thay vì nút Đăng nhập. Token được lưu trong localStorage. |
| 4 | Xem album | Nhấp vào một album, hiển thị ảnh bìa, thông tin album và danh sách bài hát. |
| 5 | Phát nhạc | Nhấn nút phát trên một bài hát, thanh Music Player xuất hiện, nhạc phát, nút play/pause hoạt động. |
| 6 | Tìm kiếm | Nhập từ khóa vào ô tìm kiếm, kết quả trả về đúng (bài hát, nghệ sĩ, album). |
| 7 | Xem MV | Vào một MV, video phát được bằng `react-player`. |
| 8 | Quản lý playlist | Tạo playlist mới, thêm bài hát vào, kiểm tra danh sách "My Playlists". |


##### 1.2. Phía quản trị (admin)

Đăng nhập với tài khoản có `is_staff=True` (hoặc dùng tài khoản admin mặc định nếu có). Truy cập `/admin` (giao diện React Admin).

| # | Tác vụ | Kết quả mong đợi |
|---|--------|------------------|
| 1 | Dashboard | Hiển thị số liệu thống kê (bài hát, MV, nghệ sĩ, người dùng) – nếu đã tích hợp API thống kê. |
| 2 | Quản lý bài hát | Thêm bài hát mới (upload file audio), sửa metadata, xóa (có xác nhận). |
| 3 | Quản lý MV | Thêm MV (video), sửa, xóa. |
| 4 | Quản lý album | Tạo album, thêm/gỡ bài hát khỏi album. |
| 5 | Quản lý nghệ sĩ | Thêm, sửa, xóa nghệ sĩ; upload ảnh đại diện. |
| 6 | Quản lý người dùng | Xem danh sách, thay đổi vai trò, khóa tài khoản, xóa. |

---

#### 2. Kiểm thử bảo mật

##### 2.1. CORS và truy cập API

- Dùng trình duyệt mở console, kiểm tra các request từ frontend (S3) đến backend (EC2). Không được có lỗi CORS policy.
- Nếu dùng `django-cors-headers` với `CORS_ALLOW_ALL_ORIGINS = True` (chỉ nên dùng tạm thời), các request sẽ thành công. Trong thực tế nên giới hạn danh sách origin.

##### 2.2. Xác thực và phân quyền

- Tắt token (xóa khỏi localStorage), thử truy cập `/admin` – phải bị chuyển hướng về login.
- Gọi API tạo playlist mà không có token (bằng Postman): server trả về `401 Unauthorized`.
- Đăng nhập với tài khoản thường, thử gọi API admin (ví dụ xóa bài hát): server trả về `403 Forbidden`.

##### 2.3. Bảo vệ tài nguyên trên AWS

- S3 bucket policy chỉ cho phép `s3:GetObject`, không cho phép upload/xóa.
- Security group của EC2 chỉ mở cổng 8000 (và 22 giới hạn IP). Kiểm tra bằng cách quét nhanh với `nmap` từ bên ngoài (tùy chọn).
- IAM user `music-app-deployer` chỉ có quyền S3 và EC2, không có quyền IAM hay RDS.


---

#### 3. Kiểm thử hiệu năng

##### 3.1. Đánh giá frontend

Sử dụng **Lighthouse** (trong Chrome DevTools) để kiểm tra điểm Performance, Accessibility, Best Practices, SEO. Mục tiêu:
- Performance: điểm > 70.
- Tối ưu ảnh: sử dụng định dạng WebP, kích thước phù hợp.
- Thời gian tải trang chủ < 3 giây.

##### 3.2. Đánh giá backend

Dùng **Postman** hoặc **ab** (Apache Benchmark) để gửi 100 request liên tiếp đến endpoint `/api/track/?category=audio`.
- Quan sát thời gian phản hồi trung bình (dưới 500ms cho mỗi request).
- Django `runserver` không được tối ưu cho nhiều request đồng thời, vì vậy đây chỉ là kiểm tra cơ bản.

##### 3.3. Cải thiện (nếu có thời gian)

- Bật caching tĩnh ở CloudFront (nếu đã dùng) với TTL dài.
- Sử dụng gzip nén dữ liệu.
- Giới hạn kích thước file upload trong admin.

---

#### 4. Dọn dẹp tài nguyên AWS

Sau khi hoàn thành kiểm thử và không còn nhu cầu sử dụng, bạn nên xóa các tài nguyên để tránh phát sinh chi phí.

##### 4.1. Terminate EC2 instance

- Vào **EC2 console → Instances**. Chọn instance `music-backend`. Nhấn **Instance state → Terminate instance**. Xác nhận.

##### 4.2. Xóa S3 bucket

- Trước khi xóa bucket, cần xóa hết object bên trong.
- Có thể dùng AWS CLI: `aws s3 rm s3://music-app-frontend --recursive`
- Sau đó xóa bucket trong console hoặc CLI: `aws s3 rb s3://music-app-frontend --force`

##### 4.3. Xóa IAM user

- Vào **IAM → Users**. Chọn `music-app-deployer`. Xóa các access key, sau đó nhấn **Delete user**.

##### 4.4. Xóa các tài nguyên khác (nếu có)

- Elastic IP: vào EC2 → Elastic IPs, release các IP chưa được gán.
- CloudFront distribution: disable và delete.
- Route 53 hosted zone: xóa các record rồi xóa zone.

Sau khi dọn dẹp, kiểm tra **Billing Dashboard** để chắc chắn không còn tài nguyên nào sinh phí.


---

#### 5. Tổng kết

Qua 6 phần của workshop:

- Xây dựng hoàn chỉnh một website nghe nhạc với React (client + admin).
- Tạo API backend bằng Django REST Framework, hỗ trợ JWT.
- Triển khai ứng dụng lên AWS S3 và EC2 (mặc dù ở mức development).
- Thực hiện kiểm thử và đảm bảo chất lượng cơ bản.
- Quản lý và dọn dẹp tài nguyên hiệu quả.

