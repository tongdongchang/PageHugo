---
title: "Worklog Tuần 8"
date: 2026-04-27
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---


### Mục tiêu tuần 8

* Tổng kết toàn bộ dự án Website nghe nhạc sau 7 tuần triển khai.
* Kiểm thử toàn diện hệ thống (frontend, backend, admin, triển khai AWS) để đảm bảo chất lượng sản phẩm.
* Hoàn thiện tài liệu kỹ thuật, hướng dẫn sử dụng và báo cáo tổng kết thực tập.
* Bàn giao sản phẩm, rút kinh nghiệm và kết thúc đợt thực tập.

### Lịch trình công việc chi tiết

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2   | - Tổ chức họp nhóm đánh giá tổng thể sản phẩm, liệt kê các phần đã hoàn thiện và tồn tại <br> - Kiểm thử chức năng từ phía người dùng cuối: đăng ký, đăng nhập, nghe nhạc, playlist, tìm kiếm, xem MV <br> - Ghi nhận lỗi, lập danh sách các vấn đề cần sửa | 27/04/2026 | 27/04/2026 | Test case mẫu, checklist |
| 3   | - Kiểm thử chức năng admin: quản lý bài hát, MV, nghệ sĩ, album, người dùng, dashboard <br> - Sửa các lỗi nhỏ phát sinh trong quá trình kiểm thử (frontend & backend) <br> - Xác nhận toàn bộ API hoạt động đúng với yêu cầu | 28/04/2026 | 28/04/2026 | Postman, Browser DevTools |
| 4   | - Rà soát bảo mật: kiểm tra phân quyền, CORS, HTTPS, bucket policy, security group <br> - Tối ưu nhẹ hiệu năng: nén hình ảnh, cache CloudFront, kiểm tra thời gian tải trang <br> - Sao lưu dữ liệu (database, media) và snapshot hệ thống | 29/04/2026 | 29/04/2026 | AWS best practices |
| 5   | - Viết tài liệu kỹ thuật: mô tả kiến trúc hệ thống, danh sách API, hướng dẫn cài đặt trên AWS <br> - Viết hướng dẫn sử dụng cho người dùng cuối (có thể kèm ảnh chụp màn hình) <br> - Tổng hợp mã nguồn, sắp xếp repository | 30/04/2026 | 30/04/2026 | README template |
| 6   | - Viết báo cáo tổng kết thực tập: tóm tắt quá trình, kết quả đạt được, khó khăn, bài học kinh nghiệm <br> - Nộp báo cáo, sản phẩm và tài liệu cho mentor/giảng viên <br> - Kết thúc đợt thực tập, lưu trữ tài nguyên AWS (tạm dừng instance nếu cần) | 01/05/2026 | 01/05/2026 | Hướng dẫn báo cáo thực tập |

### Kết quả đạt được sau tuần 8

* Toàn bộ hệ thống website nghe nhạc đã được kiểm thử và hoạt động ổn định trên môi trường production.
* Các chức năng người dùng và admin đều phản hồi đúng, không còn lỗi nghiêm trọng.
* Hệ thống đảm bảo các tiêu chí bảo mật cơ bản, hiệu năng chấp nhận được với thời gian tải trang tốt.
* Tài liệu kỹ thuật và hướng dẫn sử dụng hoàn chỉnh, dễ hiểu, hỗ trợ bảo trì và mở rộng về sau.
* Báo cáo thực tập được hoàn thành, trình bày đầy đủ quá trình, thành quả và kinh nghiệm thu được.
* Dự án kết thúc đúng tiến độ, các thành viên rút ra nhiều bài học quý báu về phát triển full‑stack và triển khai trên AWS.