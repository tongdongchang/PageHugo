---
title: "Worklog Tuần 5"
date: 2026-04-06
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5

* Xây dựng backend Django để cung cấp API cho phía client (website nghe nhạc).
* Hoàn thiện các API phục vụ: lấy dữ liệu, thêm, sửa, xóa cho người dùng cuối (không bao gồm API cho trang quản trị).
* Đảm bảo API có xác thực người dùng, phân quyền, tìm kiếm và sẵn sàng tích hợp với frontend React.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Khởi tạo dự án Django và app `music_api` <br> - Cấu hình Django REST Framework, JWT (JSON Web Token) cho xác thực <br> - Thiết kế models: Song, Artist, Album, Playlist, PlaylistSong, User (tùy chỉnh nếu cần) <br> - Tạo và chạy migrations | 06/04/2026 | 06/04/2026 | Django Docs, DRF Docs, Simple JWT |
| 3   | - Viết serializers cho các model (Song, Artist, Album, Playlist, User) <br> - Xây dựng API views cơ bản: list/detail cho Song, Artist, Album (chỉ đọc) <br> - Thiết lập URL routing cho các endpoint trên | 07/04/2026 | 07/04/2026 | DRF Serializers, Generic Views |
| 4   | - Tạo endpoint đăng ký (`/api/register/`) và đăng nhập (`/api/token/`) sử dụng JWT <br> - Cài đặt phân quyền: chỉ user đã xác thực mới được quản lý playlist <br> - Xây dựng Playlist API: list playlist của user, tạo mới, thêm/xóa bài hát khỏi playlist | 08/04/2026 | 08/04/2026 | DRF Authentication, ViewSets |
| 5   | - Phát triển API tìm kiếm: lọc bài hát theo tên, nghệ sĩ, album <br> - Tích hợp phân trang và bộ lọc cho danh sách bài hát, album <br> - Kiểm tra toàn bộ API bằng Browsable API và Postman | 09/04/2026 | 09/04/2026 | DRF Filtering, django-filter |
| 6   | - Cấu hình phục vụ file tĩnh/media cho audio (MEDIA_URL) <br> - Rà soát mã nguồn, tối ưu truy vấn, xử lý lỗi <br> - Viết báo cáo tuần 5 | 10/04/2026 | 10/04/2026 | Django Static/Media, Tài liệu tổng hợp |

### Kết quả đạt được sau tuần 5

* Đã xây dựng thành công backend Django với các API cốt lõi phục vụ client nghe nhạc:
  * API bài hát (Song): danh sách, chi tiết, hỗ trợ tìm kiếm và phân trang.
  * API nghệ sĩ (Artist): danh sách, chi tiết, kèm danh sách album/bài hát liên quan.
  * API album (Album): danh sách, chi tiết album và danh sách bài hát bên trong.
  * API playlist: quản lý playlist cá nhân của người dùng (tạo, sửa, xóa, thêm/xóa bài hát).
* Hệ thống xác thực người dùng hoạt động với JWT: đăng ký, đăng nhập, bảo vệ các API yêu cầu quyền riêng tư.
* Mỗi API đều có đầy đủ phân quyền (read-only với nội dung chính, quyền ghi chỉ trên playlist của chính người dùng đó).
* Tính năng tìm kiếm cho phép lọc bài hát theo tên, nghệ sĩ, album; hỗ trợ gợi ý và phân trang.
* Đã cấu hình phục vụ file tĩnh/media, đảm bảo client có thể stream audio từ server Django (nếu có).
* Toàn bộ API đã được kiểm thử bằng Postman và sẵn sàng kết nối với giao diện React đã xây dựng trước đó.