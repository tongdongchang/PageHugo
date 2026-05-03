---
title: "Worklog Tuần 6"
date: 2026-04-13
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6

* Xây dựng API dành riêng cho trang quản trị (Admin Panel) của website nghe nhạc.
* Hoàn thiện các endpoint quản lý: audio (bài hát), MV, nghệ sĩ, album và người dùng với đầy đủ CRUD.
* Phát triển API thống kê tổng quan cho dashboard admin.
* Áp dụng cơ chế xác thực và phân quyền admin nghiêm ngặt.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Tạo app `admin_api` trong Django project, tách biệt với API client <br> - Thiết lập quyền truy cập admin: chỉ user có `is_staff=True` mới được gọi <br> - Xây dựng API quản lý Audio (Song): list (phân trang), tạo (upload file), sửa, xóa | 13/04/2026 | 13/04/2026 | DRF Permissions, Django File Upload |
| 3   | - Xây dựng API quản lý MV: CRUD, hỗ trợ upload video hoặc nhập URL <br> - Tích hợp xác thực file (định dạng, dung lượng) khi upload <br> - Kiểm tra endpoint bằng Postman | 14/04/2026 | 14/04/2026 | DRF FileUploadParser, Validation |
| 4   | - Xây dựng API quản lý Nghệ sĩ (Artist): CRUD, upload ảnh đại diện, xử lý liên kết album <br> - Xây dựng API quản lý Album: CRUD, thêm/xóa bài hát vào album, cập nhật ảnh bìa | 15/04/2026 | 15/04/2026 | Nested Relationships, DRF Viewsets |
| 5   | - Xây dựng API quản lý Người dùng (User): danh sách (có tìm kiếm/lọc), cập nhật vai trò, khóa/mở khóa tài khoản, xóa <br> - Viết API thống kê Dashboard: số lượng bài hát, MV, nghệ sĩ, người dùng, playlist; bài hát mới nhất,... | 16/04/2026 | 16/04/2026 | DRF Filtering, Aggregation |
| 6   | - Rà soát bảo mật: kiểm tra lại tất cả permission, tránh leo quyền <br> - Viết tài liệu API ngắn (swagger/redoc nếu có) <br> - Tổng kết tuần 6, viết báo cáo | 17/04/2026 | 17/04/2026 | DRF Docs, drf-yasg, Tài liệu tổng hợp |

### Kết quả đạt được sau tuần 6

* Hoàn thiện toàn bộ API cho trang admin, sẵn sàng phục vụ giao diện quản trị React.
* Đã xây dựng được các cụm API chính:
  * **Audio Admin API**: quản lý toàn bộ bài hát (thêm, sửa, xóa, upload file mp3), hỗ trợ phân trang và lọc.
  * **MV Admin API**: quản lý video nhạc, hỗ trợ upload/link, xác thực định dạng, cập nhật trạng thái.
  * **Artist Admin API**: CRUD nghệ sĩ, upload ảnh, liên kết nhanh album – đảm bảo tính nhất quán dữ liệu.
  * **Album Admin API**: CRUD album, quản lý bài hát trong album, thay ảnh bìa.
  * **User Admin API**: quản lý người dùng toàn hệ thống, phân quyền, khóa tài khoản.
* API Dashboard cung cấp dữ liệu thống kê thời gian thực cho trang tổng quan admin.
* Hệ thống phân quyền admin hoạt động chính xác: chỉ tài khoản được cấp quyền `staff` mới truy cập được các endpoint admin, ngăn chặn truy cập trái phép.
* Tất cả endpoint đều có validate dữ liệu đầu vào, phản hồi lỗi rõ ràng, tuân thủ chuẩn RESTful.
* Bộ API đã được kiểm thử qua Postman và sẵn sàng tích hợp với giao diện Admin React đã xây dựng ở tuần 4.