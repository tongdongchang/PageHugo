---
title : "Xây dựng giao diện quản trị"
date : 2026-05-01
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---


### Mục tiêu

Xây dựng giao diện quản trị (Admin Panel) để kiểm soát toàn bộ dữ liệu của website nghe nhạc. Giao diện được xây dựng bằng React và Ant Design, bao gồm các chức năng thêm, sửa, xóa cho bài hát, album, nghệ sĩ và người dùng. Chỉ những tài khoản có quyền admin mới được truy cập khu vực này.

---

#### 1. Cấu trúc thư mục Admin

Các file được tổ chức trong thư mục `src/admin/` như sau:
src/admin/
├── Admin.jsx # Layout quản trị (sidebar + nội dung)
├── Album.jsx # Danh sách album, thêm/sửa/xóa
├── Artists.jsx # Quản lý nghệ sĩ
├── DetailAlbum.jsx # Chi tiết một album (thêm/gỡ bài hát)
├── SliderAdmin.jsx # Sidebar điều hướng
├── Track.jsx # Quản lý bài hát (audio)
└── Users.jsx # Quản lý người dùng

text

Tất cả đều được import và sử dụng trong cây route của React Router.

---

#### 2. Layout quản trị (`Admin.jsx` và `SliderAdmin.jsx`)

- **SliderAdmin.jsx** cung cấp thanh điều hướng dọc bên trái, sử dụng `Menu` của Ant Design. Các mục chính:
  - Quản lý bài hát (`/admin/tracks`)
  - Quản lý album (`/admin/albums`)
  - Quản lý nghệ sĩ (`/admin/artists`)
  - Quản lý người dùng (`/admin/users`)

- **Admin.jsx** sử dụng `Layout` của Ant Design, chia thành `Sider` (sidebar) và `Content`. Nó bao bọc `<Outlet />` để hiển thị trang tương ứng. Code mẫu:

```jsx
import { Outlet } from 'react-router-dom';
import { Layout } from 'antd';
import SliderAdmin from './SliderAdmin';

const { Content } = Layout;

const Admin = () => (
  <Layout style={{ minHeight: '100vh' }}>
    <SliderAdmin />
    <Layout>
      <Content style={{ margin: '24px' }}>
        <Outlet />
      </Content>
    </Layout>
  </Layout>
);

export default Admin;
```
### 3. Các trang quản lý chi tiết

#### 3.1. Quản lý bài hát (Track.jsx)

Hiển thị danh sách bài hát dưới dạng bảng (Ant Design Table) với các cột: Tên bài hát, Nghệ sĩ, Album, Thời lượng, Hành động.

Nút **Thêm mới** mở một Modal chứa Form cho phép:

* Nhập tên bài, chọn nghệ sĩ và album từ danh sách có sẵn
* Upload file audio (giả lập, thực tế sẽ gửi file lên server sau khi tích hợp API)
* Nhập thời lượng hoặc tự động lấy từ file

Mỗi dòng có:

* Nút **Sửa** (mở modal với dữ liệu đã điền sẵn)
* Nút **Xóa** kèm xác nhận (Popconfirm)

![Giao diện quản lý bài hát](/images/5-Workshop/5.3-S3-vpc/track.png)   

---

#### 3.2. Quản lý album (Album.jsx)

Bảng danh sách album gồm:

* Tên album
* Nghệ sĩ
* Số bài hát
* Ảnh bìa

Thêm/Sửa album thông qua Modal:

* Nhập tên album, chọn nghệ sĩ
* Upload ảnh bìa

Sau khi tạo mới, có thể chuyển sang **DetailAlbum** để thêm bài hát.

Nút Xóa album sẽ hiển thị cảnh báo nếu album đang chứa bài hát.
![Giao diện quản lý album](/images/5-Workshop/5.3-S3-vpc/albumadmin.png)   

---

#### 3.3. Chi tiết album (DetailAlbum.jsx)

Nhận `id` album từ URL.

Hiển thị:

* Ảnh bìa
* Tên album
* Nghệ sĩ

Hai khu vực chính:

* Danh sách bài hát trong album (có nút gỡ)
* Danh sách tất cả bài hát (có tìm kiếm để thêm)

Có thể dùng:

* `Transfer`
* Hoặc 2 bảng + nút thêm/gỡ

![Chi tiết album](/images/5-Workshop/5.3-S3-vpc/detailablum.png)

---

#### 3.4. Quản lý nghệ sĩ (Artists.jsx)

Bảng danh sách:

* Tên
* Tiểu sử (rút gọn)
* Ảnh đại diện

Modal thêm/sửa:

* Nhập tên, tiểu sử
* Upload ảnh

Nút Xóa có xác nhận. Khi xóa cần kiểm tra ràng buộc với album/bài hát.
![Quản lý nghệ sĩ](/images/5-Workshop/5.3-S3-vpc/artist.png)

---

#### 3.5. Quản lý người dùng (Users.jsx)

Bảng danh sách:

* Tên người dùng
* Email
* Vai trò (Admin/User)
* Trạng thái (Hoạt động/Bị khóa)

Chức năng:

* Đổi vai trò (Admin/User)
* Khóa/Mở khóa tài khoản
* Xóa người dùng (có xác nhận)

![Quản lý người dùng](/images/5-Workshop/5.3.2-admin-frontend/admin-users.png)

---

### 4. Bảo vệ route Admin

Để ngăn người dùng thường truy cập, bọc route admin bằng component kiểm tra quyền:

```jsx
import { Navigate } from 'react-router-dom';
import { useAuth } from '../contexts/AuthContext';

const AdminRoute = ({ children }) => {
  const { user } = useAuth();
  return user?.role === 'admin' ? children : <Navigate to="/login" />;
};

// Sử dụng
<Route path="/admin" element={<AdminRoute><Admin /></AdminRoute>}>
  ...
</Route>
```

---

### 5. Kết quả

Sau khi hoàn thành, khu vực quản trị cho phép kiểm soát toàn bộ nội dung website thông qua giao diện trực quan, nhất quán với Ant Design.

Mọi thao tác thêm, sửa, xóa đều có phản hồi rõ ràng và an toàn.
