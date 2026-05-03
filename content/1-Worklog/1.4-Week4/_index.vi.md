---
title: "Worklog Tuần 4"
date: 2026-03-30
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---


### Mục tiêu tuần 4

* Phát triển giao diện quản trị (Admin Panel) cho website nghe nhạc.
* Hoàn thiện các chức năng quản lý: audio (bài hát), MV, nghệ sĩ, album và người dùng (thêm, sửa, xóa).
* Xây dựng dashboard trực quan, đảm bảo thao tác thuận tiện và sẵn sàng kết nối API.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Tạo khu vực Admin trong dự án React (route `/admin`), bố cục sidebar + main content <br> - Thiết kế trang quản lý Audio: bảng danh sách bài hát, form thêm/chỉnh sửa (upload file, metadata), nút xóa <br> - Sử dụng mock data cho Audio | 30/03/2026 | 30/03/2026 | React Router, Ant Design / Material UI (docs) |
| 3   | - Xây dựng trang quản lý MV: hiển thị danh sách MV, form upload/link video, sửa thông tin, xóa <br> - Tương tự, tích hợp React Hook Form và quản lý trạng thái <br> - Mock data cho MV | 31/03/2026 | 31/03/2026 | React Hook Form, API upload (giả lập) |
| 4   | - Phát triển quản lý Nghệ sĩ (Artists): CRUD tên, tiểu sử, ảnh đại diện, liên kết album <br> - Quản lý Album: tạo album, thêm bài hát vào album, sửa thông tin, xóa <br> - Các form và bảng dùng chung component tái sử dụng | 01/04/2026 | 01/04/2026 | Component reuse patterns |
| 5   | - Xây dựng trang quản lý Người dùng (Users): danh sách, thay đổi vai trò (admin/user), khóa/mở khóa tài khoản, xóa <br> - Tạo Dashboard tổng quan: thống kê số lượng bài hát, MV, nghệ sĩ, người dùng (mock) | 02/04/2026 | 02/04/2026 | Thư viện biểu đồ (recharts), mock data |
| 6   | - Rà soát toàn bộ giao diện Admin, đảm bảo validation, responsive, thông báo lỗi/thành công <br> - Viết báo cáo tuần 4 và cập nhật tiến độ với nhóm | 03/04/2026 | 03/04/2026 | Tài liệu tổng hợp |

### Kết quả đạt được sau tuần 4

* Hoàn thành giao diện quản trị với đầy đủ các chức năng quản lý dữ liệu cốt lõi.
* Trang quản lý Audio: hiển thị danh sách bài hát, hỗ trợ thêm mới (upload file giả lập), chỉnh sửa metadata, xóa bài hát kèm xác nhận.
* Trang quản lý MV: quản lý video âm nhạc tương tự, bao gồm nhập link hoặc chọn file, mô tả MV, xóa an toàn.
* Trang quản lý Nghệ sĩ: CRUD đầy đủ, upload ảnh đại diện, liên kết nhanh đến album của nghệ sĩ.
* Trang quản lý Album: tạo album mới, thêm/xóa bài hát khỏi album, sửa thông tin album, xóa album.
* Trang quản lý Người dùng: danh sách người dùng phân trang, thay đổi quyền, khóa tài khoản, xóa người dùng.
* Dashboard cung cấp cái nhìn tổng quan với các số liệu thống kê chính (dữ liệu mock), giao diện trực quan.
* Tất cả các trang đều có xác thực dữ liệu nhập, phản hồi trạng thái (loading, error, success), và tương thích responsive cơ bản, sẵn sàng thay thế mock data bằng API thật.