---
title: "Worklog Tuần 7"
date: 2026-04-20
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7

* Triển khai ứng dụng web nghe nhạc lên AWS với ba dịch vụ chính: S3, CloudFront và Route 53 cho frontend; EC2 cho backend.
* Lưu trữ giao diện React trên S3, phân phối qua CloudFront và quản lý tên miền tùy chỉnh bằng Route 53.
* Cấu hình máy chủ ảo EC2 chạy backend Django, phục vụ API và file tĩnh/media.
* Đảm bảo toàn bộ hệ thống hoạt động an toàn, ổn định trên môi trường production với HTTPS.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Build production React bằng Vite, kiểm tra biến môi trường (API URL) <br> - Tạo S3 bucket, kích hoạt tính năng static website hosting, cấu hình bucket policy <br> - Upload toàn bộ thư mục build (`dist`) lên bucket, xác nhận truy cập qua endpoint mặc định | 20/04/2026 | 20/04/2026 | AWS S3 Docs, Vite build guide |
| 3   | - Tạo CloudFront distribution với origin là S3 bucket, bật redirect HTTP sang HTTPS <br> - Cấu hình custom error response (403 -> 200) để hỗ trợ SPA routing <br> - Yêu cầu chứng chỉ SSL công khai qua AWS Certificate Manager, xác thực tên miền <br> - Tạo hosted zone trên Route 53 (nếu chưa có), thêm bản ghi A (Alias) trỏ đến CloudFront distribution | 21/04/2026 | 21/04/2026 | AWS CloudFront, ACM, Route 53 docs |
| 4   | - Khởi tạo EC2 instance (Ubuntu), cấu hình security group mở cổng 80/443 và SSH <br> - Cài đặt Python, virtualenv, clone mã nguồn Django, cấu hình database (PostgreSQL cục bộ hoặc RDS nếu yêu cầu) <br> - Cài Gunicorn, tạo service systemd để chạy Django ổn định | 22/04/2026 | 22/04/2026 | AWS EC2 Docs, Django deployment guide |
| 5   | - Cài đặt Nginx làm reverse proxy cho Gunicorn, cấu hình phục vụ file tĩnh/media <br> - Thiết lập HTTPS cho backend bằng Let’s Encrypt (certbot) hoặc AWS Certificate Manager nếu dùng Load Balancer <br> - Cập nhật CORS và ALLOWED_HOSTS trong Django, kiểm tra API hoạt động qua HTTPS | 23/04/2026 | 23/04/2026 | Nginx, Let’s Encrypt, DRF CORS |
| 6   | - Cập nhật biến môi trường React build mới (API URL trỏ đến domain backend) và tải lại lên S3, invalidate CloudFront cache nếu cần <br> - Kiểm tra toàn bộ luồng: frontend (qua domain) gọi API backend thành công, đăng nhập, nghe nhạc, quản trị <br> - Viết báo cáo tuần 7, liệt kê vấn đề và đề xuất cải tiến | 24/04/2026 | 24/04/2026 | Tài liệu tổng hợp |

### Kết quả đạt được sau tuần 7

* Frontend React được lưu trữ trên S3, phân phối toàn cầu qua CloudFront với tốc độ cao, hỗ trợ HTTPS và tên miền riêng quản lý bởi Route 53.
* Backend Django chạy trên EC2:
  * Gunicorn + Nginx đảm bảo xử lý API ổn định và phục vụ file tĩnh.
  * Database hoạt động tin cậy (PostgreSQL hoặc SQLite phù hợp môi trường).
  * HTTPS được kích hoạt thông qua Let’s Encrypt hoặc ACM, bảo mật dữ liệu truyền tải.
* Toàn bộ website hoạt động trơn tru qua tên miền thật, frontend và backend giao tiếp không lỗi.
* Các biện pháp bảo mật cơ bản đã được triển khai: security group giới hạn cổng, bucket policy hạn chế truy cập công khai không cần thiết, giao thức HTTPS bắt buộc.
* Sẵn sàng cho các giai đoạn tiếp theo như giám sát (CloudWatch), CI/CD, tự động sao lưu và tối ưu chi phí.