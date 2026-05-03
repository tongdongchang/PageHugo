---
title: "Worklog Tuần 2"
date: 2026-03-16
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---


### Mục tiêu tuần 2

* Gặp gỡ, trao đổi với nhóm về dự án "Website nghe nhạc".
* Nghiên cứu tổng quan về công nghệ sử dụng: React (frontend) và Django (backend).
* Nắm được kiến trúc cơ bản và luồng dữ liệu giữa các thành phần (chưa code).

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Tham gia họp nhóm, giới thiệu thành viên và phân chia nhiệm vụ ban đầu <br> - Xem lại các quy chế, nội quy thực tập | 16/03/2026 | 16/03/2026 | Tài liệu nội bộ |
| 3   | - Tìm hiểu đề bài "Website nghe nhạc": các tính năng chính (nghe nhạc, playlist, tìm kiếm,...) <br> - Tổng quan về công nghệ React và Django, lý do lựa chọn | 17/03/2026 | 17/03/2026 | React Docs, Django Docs |
| 4   | - Nghiên cứu sâu hơn về React: JSX, component, state, hooks, cách tổ chức dự án <br> - Xem các mẫu giao diện nghe nhạc phổ biến để tham khảo | 18/03/2026 | 18/03/2026 | React Docs, Figma mẫu |
| 5   | - Tìm hiểu Django: Models, Views, Templates (nếu có), Django REST Framework <br> - Thiết kế sơ bộ cơ sở dữ liệu cho bài toán nghe nhạc (bài hát, ca sĩ, album,...) | 19/03/2026 | 19/03/2026 | Django Docs, DRF Docs |
| 6   | - Nghiên cứu cách kết nối giữa React và Django REST API <br> - Tìm hiểu cơ chế streaming nhạc, xử lý file audio, bảo mật API | 20/03/2026 | 20/03/2026 | REST API best practices |

### Kết quả đạt được sau tuần 2

* Hiểu rõ mục tiêu dự án "Website nghe nhạc" và các tính năng cần có.
* Nắm vững kiến thức nền tảng về React:
  * Cấu trúc component, quản lý state bằng hooks
  * Tổ chức thư mục dự án frontend
  * Các thư viện UI phổ biến hỗ trợ xây dựng giao diện nghe nhạc

* Nắm vững kiến thức nền tảng về Django:
  * Mô hình MTV (Model – Template – View) và Django REST Framework
  * Thiết kế CSDL sơ bộ bao gồm các bảng: Song, Artist, Album, Playlist, User
  * Cách tạo API CRUD cơ bản

* Biết cách kết nối frontend và backend thông qua REST API, hiểu luồng dữ liệu:
  * React gửi HTTP request đến Django backend
  * Django xử lý, truy vấn database và trả về JSON

* Khám phá một số thách thức kỹ thuật như streaming nhạc, quản lý file media, xác thực người dùng, bảo mật API.

* Sẵn sàng cho giai đoạn tiếp theo: bắt đầu code các chức năng đầu tiên.