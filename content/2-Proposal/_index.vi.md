---
title: "Bản đề xuất"
date: 2026-03-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Website nghe nhạc trực tuyến  
## Nền tảng full‑stack với React, Django và hạ tầng AWS  

### 1. Tóm tắt điều hành  
Website nghe nhạc được phát triển trong khuôn khổ chương trình **First Cloud Journey** nhằm cung cấp một ứng dụng web hoàn chỉnh cho người dùng nghe nhạc, quản lý playlist, xem MV và tìm kiếm nghệ sĩ/album. Dự án sử dụng React (giao diện người dùng) và Django (API phụ trợ), được triển khai trên các dịch vụ AWS như S3, CloudFront, Route 53 và EC2. Ngoài giao diện người dùng, hệ thống còn bao gồm trang quản trị riêng để quản lý bài hát, MV, nghệ sĩ, album và người dùng. Mục tiêu là hoàn thiện một sản phẩm thực tế trong **8 tuần**, giúp nhóm thực tập sinh nắm vững kỹ năng phát triển full‑stack và triển khai trên đám mây.

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Việc xây dựng một website nghe nhạc hoàn chỉnh đòi hỏi kiến thức về cả frontend, backend và triển khai trên môi trường production. Các giải pháp có sẵn thường phức tạp, chi phí cao hoặc không cho phép tùy biến sâu. Nhóm thực tập cần một dự án thực tế để rèn luyện kỹ năng nhưng vẫn nằm trong nguồn lực hạn chế (Free Tier AWS và công cụ mã nguồn mở).

*Giải pháp*  
Xây dựng một website nghe nhạc từ đầu, sử dụng:
- **React** (Vite) để tạo giao diện người dùng và giao diện quản trị, hỗ trợ phát nhạc, tìm kiếm, quản lý playlist.
- **Django REST Framework** để phát triển API cho cả client và admin, xác thực người dùng bằng JWT.
- **AWS** để triển khai: S3 + CloudFront + Route 53 cho frontend tĩnh, EC2 cho backend Django.
Giải pháp tập trung vào kiến trúc đơn giản, dễ mở rộng, tiết kiệm chi phí và phù hợp cho môi trường học tập/nghiên cứu.

*Lợi ích và hoàn vốn đầu tư (ROI)*  
- Sinh viên có sản phẩm thực tế để đưa vào báo cáo và portfolio.
- Nắm vững quy trình phát triển full‑stack và triển khai trên AWS.
- Chi phí hạ tầng hầu như bằng 0 khi tận dụng AWS Free Tier trong thời gian thực tập.
- Nền tảng có thể được sử dụng làm mẫu cho các dự án tương tự trong tương lai.

### 3. Kiến trúc giải pháp  
Toàn bộ hệ thống được chia thành hai khối chính:

- **Frontend**: Ứng dụng React (Single Page Application) được build thành tệp tĩnh, lưu trên S3 và phân phối qua CloudFront. Tên miền tuỳ chỉnh trỏ đến CloudFront thông qua Route 53.
- **Backend**: Django chạy trên máy ảo EC2, đảm nhận xử lý API, xác thực và phục vụ file media. API được bảo vệ bởi JWT, riêng API quản trị yêu cầu quyền staff.

*Dịch vụ AWS sử dụng*
- **Amazon S3**: Lưu trữ giao diện React tĩnh.
- **Amazon CloudFront**: CDN tăng tốc và hỗ trợ HTTPS cho frontend.
- **Amazon Route 53**: Quản lý tên miền và định tuyến đến CloudFront.
- **Amazon EC2**: Máy chủ ảo chạy Django + Gunicorn + Nginx.
- *(Tuỳ chọn)* **Amazon RDS**: Cơ sở dữ liệu PostgreSQL nếu cần mở rộng.
- **AWS Certificate Manager**: Cung cấp chứng chỉ SSL miễn phí cho tên miền.

*Thiết kế thành phần*
- **Giao diện người dùng**: Trang chủ, Đăng ký/Đăng nhập, Album, Playlist, Music Player, Tìm kiếm, Xem MV.
- **Giao diện quản trị**: Quản lý bài hát, MV, nghệ sĩ, album, người dùng, Dashboard thống kê.
- **API Client**: Endpoint danh sách bài hát/album/nghệ sĩ (có phân trang, tìm kiếm), đăng ký/đăng nhập (JWT), quản lý playlist cá nhân.
- **API Admin**: CRUD toàn bộ tài nguyên, dashboard.

### 4. Triển khai kỹ thuật  
Dự án được triển khai theo lộ trình 8 tuần:

| Tuần | Nội dung | Công nghệ chính |
|------|----------|-----------------|
| 1    | Làm quen AWS, tạo tài khoản Free Tier, thực hành EC2, S3, CLI | AWS Console, CLI |
| 2    | Nghiên cứu dự án: yêu cầu website nghe nhạc, công nghệ React, Django | React docs, Django docs |
| 3    | Xây dựng toàn bộ giao diện người dùng (React) | React, React Router, Context API, CSS |
| 4    | Xây dựng giao diện quản trị (React Admin) | React, Ant Design/Material UI |
| 5    | Phát triển API cho client (Django) | DRF, JWT, PostgreSQL/SQLite |
| 6    | Phát triển API cho admin (Django) | DRF, Permissions, Upload file |
| 7    | Triển khai lên AWS: frontend lên S3 + CloudFront + Route 53, backend lên EC2 | S3, CloudFront, Route 53, EC2, Nginx, Gunicorn, SSL |
| 8    | Kiểm thử toàn diện, viết tài liệu, tổng kết | Postman, Test case, README |

*Yêu cầu kỹ thuật*
- **Frontend**: Node.js, Vite, React 18+, React Router, React Hook Form.
- **Backend**: Python 3.10+, Django 4.x, Django REST Framework, Simple JWT.
- **Triển khai**: Ubuntu EC2, Nginx, Gunicorn, SSL (Let's Encrypt hoặc ACM).
- **Cơ sở dữ liệu**: SQLite (phát triển) hoặc PostgreSQL (production).
- **Bảo mật**: HTTPS, JWT, CORS, Security Groups, Bucket Policies.

### 5. Lộ trình & Mốc triển khai
- **Trước thực tập**: Tìm hiểu trước React và Django cơ bản (2–3 tuần).
- **Thực tập (8 tuần)**:
  - Tuần 1–2: AWS cơ bản, nghiên cứu công nghệ.
  - Tuần 3–4: Hoàn thiện giao diện người dùng và quản trị.
  - Tuần 5–6: Hoàn thiện API client và admin.
  - Tuần 7: Triển khai production.
  - Tuần 8: Kiểm thử, báo cáo, kết thúc.
- **Sau triển khai**: Có thể tiếp tục bảo trì, mở rộng chức năng nếu cần.

### 6. Ước tính ngân sách  
Do tận dụng AWS Free Tier trong suốt 12 tháng đầu, chi phí dự kiến rất thấp:

| Dịch vụ              | Chi phí ước tính/tháng | Ghi chú                                      |
|----------------------|------------------------|----------------------------------------------|
| S3 (Standard)        | 0,02 USD               | Lưu trữ ít (< 1 GB)                          |
| CloudFront           | 0,00 USD               | 1 TB data transfer miễn phí (Free Tier)      |
| Route 53             | 0,50 USD               | Hosted zone                                   |
| EC2 (t2.micro)       | 0,00 USD               | Miễn phí 750 giờ/tháng trong 12 tháng        |
| Tổng                 | **~0,52 USD/tháng**    | ≈ 6,24 USD/12 tháng                          |

Không phát sinh chi phí phần cứng. Tất cả đều sử dụng tài khoản cá nhân và máy tính cá nhân.

### 7. Đánh giá rủi ro  
*Ma trận rủi ro*
- **Trễ tiến độ do lỗi kỹ thuật**: Ảnh hưởng cao, xác suất trung bình.
- **Chi phí vượt ngoài dự kiến**: Ảnh hưởng thấp, xác suất thấp (Free Tier giới hạn cứng).
- **Kiến thức hạn chế về AWS**: Ảnh hưởng trung bình, xác suất cao.

*Chiến lược giảm thiểu*
- Lên kế hoạch chi tiết từng ngày, dành buffer cho các tuần cuối.
- Theo dõi chi phí hàng ngày qua AWS Budgets, giới hạn dịch vụ ngoài Free Tier.
- Học AWS thông qua workshop của First Cloud Journey, sử dụng tài liệu chính thống.

*Kế hoạch dự phòng*
- Nếu EC2 gặp sự cố, có thể quay về chạy local để demo chức năng.
- Luôn sao lưu source code trên GitHub và backup database (nếu có) định kỳ.

### 8. Kết quả kỳ vọng  
*Kỹ năng đạt được*
- Thành thạo phát triển web full‑stack với React và Django.
- Nắm vững quy trình triển khai ứng dụng lên AWS (S3, CloudFront, Route 53, EC2).
- Có sản phẩm thực tế minh hoạ cho năng lực.

*Sản phẩm bàn giao*
- Mã nguồn frontend và backend (GitHub).
- Website hoạt động trực tuyến với đầy đủ chức năng người dùng và quản trị.
- Tài liệu kỹ thuật, hướng dẫn sử dụng và báo cáo thực tập (8 tuần).