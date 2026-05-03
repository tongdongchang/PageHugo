---
title: "Worklog Tuần 3"
date: 2026-03-23
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---


### Mục tiêu tuần 3

* Xây dựng giao diện người dùng chính cho website nghe nhạc bằng React.
* Hoàn thiện các trang: trang chủ, đăng ký, đăng nhập, album, playlist, nghe nhạc (music player bar), tìm kiếm, xem MV.
* Tạo ra một bộ khung frontend liền mạch, sẵn sàng kết nối với backend Django.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Khởi tạo dự án React với Vite, cài đặt React Router, cấu trúc thư mục <br> - Xây dựng layout chung (Header, Footer, Container) <br> - Thiết kế giao diện trang chủ: banner, danh sách bài hát gợi ý, nghệ sĩ nổi bật (dữ liệu mock) | 23/03/2026 | 23/03/2026 | React Docs, React Router Docs |
| 3   | - Tạo trang Đăng ký (Register) và Đăng nhập (Login) với form, validation cơ bản <br> - Tích hợp React Hook Form để quản lý biểu mẫu <br> - Style cho các trang auth, xử lý trạng thái lỗi, loading | 24/03/2026 | 24/03/2026 | React Hook Form Docs, CSS Modules |
| 4   | - Xây dựng trang Album chi tiết: hiển thị thông tin album, danh sách bài hát, ảnh bìa <br> - Xây dựng trang Playlist tương tự album, có chức năng thêm/xóa bài hát khỏi playlist (mock) <br> - Kết nối dữ liệu từ file JSON giả lập | 25/03/2026 | 25/03/2026 | React Context API, JSX |
| 5   | - Phát triển Music Player Bar (thanh phát nhạc) luôn hiển thị ở bottom: nút play/pause, next/prev, progress bar, volume control <br> - Tạo giao diện tìm kiếm: ô input tìm kiếm theo tên bài hát/nghệ sĩ, hiển thị kết quả dạng list <br> - Quản lý trạng thái toàn cục cho bài hát hiện tại bằng Context | 26/03/2026 | 26/03/2026 | React Context API, Audio API (Web) |
| 6   | - Xây dựng trang xem MV (Music Video): nhúng video player (ReactPlayer), hiển thị thông tin MV, danh sách MV liên quan <br> - Rà soát tổng thể các trang, đảm bảo responsive trên mobile/tablet <br> - Viết báo cáo kết quả tuần 3 | 27/03/2026 | 27/03/2026 | ReactPlayer Docs, Responsive Design |

### Kết quả đạt được sau tuần 3

* Hoàn thiện giao diện frontend cơ bản cho toàn bộ luồng chính của website nghe nhạc.
* Trang chủ hiển thị được các section gợi ý nội dung, banner bắt mắt, điều hướng rõ ràng.
* Trang đăng ký và đăng nhập có form đầy đủ, xác thực phía client, giao diện thân thiện với người dùng.
* Trang album và playlist:
  * Thể hiện chi tiết tập hợp bài hát, ảnh bìa, thông tin mô tả.
  * Cho phép thêm/xóa bài hát trong playlist một cách trực quan (mock).
* Music Player Bar:
  * Điều khiển phát nhạc với các nút cơ bản, thanh tiến trình, điều chỉnh âm lượng.
  * Đồng bộ trạng thái bài hát hiện tại trên toàn ứng dụng.
* Giao diện tìm kiếm hoạt động, lọc kết quả theo từ khóa và hiển thị nhanh.
* Trang xem MV có khả năng phát video, bố cục rõ ràng, sẵn sàng nhận dữ liệu thực từ backend.
* Toàn bộ giao diện đã được kiểm tra responsive cơ bản, sẵn sàng tích hợp API và phát triển chức năng nâng cao ở tuần tiếp theo.