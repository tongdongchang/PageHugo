---
title : "Xây dựng giao diện người dùng"
date : 2026-05-01
weight : 1
chapter : false
pre : " <b> 4.3.1. </b> "
---


### Mục tiêu

Tạo ra giao diện người dùng hoàn chỉnh cho website nghe nhạc, bao gồm các trang công khai và các component dùng chung như Header, Footer, Music Player. Sau phần này, người dùng có thể duyệt nhạc, nghe thử, tạo playlist (mock), tìm kiếm và xem MV.

---

#### 1. Khởi tạo dự án và cài đặt thư viện

```bash
npm create vite@latest frontend -- --template react
cd frontend
npm install
npm install react-router-dom react-hook-form @ant-design/icons react-player
npm run dev
```
#### 2. Cấu trúc thư mục

Các file trong `src/components/` (dựa trên danh sách thực tế):

```text
src/components/
├── Alert.jsx
├── Footer.jsx
├── GetToken.jsx
├── Head.jsx
├── Home.jsx
├── Login.jsx
├── Main.jsx
├── MusicPlayer.jsx
├── PayPal.jsx
├── PlayList.jsx
├── PlayVideoMusic.jsx
├── Register.jsx
├── Search.jsx
├── Slider.jsx
└── UserPlaylist.jsx
```
#### 3. Routes và Layout chính (Main.jsx)

`Main.jsx` đóng vai trò layout chung, chứa Header, Footer và nhúng `<Outlet />` cho nội dung trang.

```jsx
import { Outlet } from 'react-router-dom';
import Head from './Head';
import Footer from './Footer';
import MusicPlayer from './MusicPlayer';

const Main = () => (
  <>
    <Head />
    <main style={{ minHeight: '80vh' }}>
      <Outlet />
    </main>
    <Footer />
    <MusicPlayer />
  </>
);

export default Main;
```

Trong `App.jsx`, cấu hình routes cho phần người dùng:

```jsx
<Route path="/" element={<Main />}>
  <Route index element={<Home />} />
  <Route path="login" element={<Login />} />
  <Route path="register" element={<Register />} />
  <Route path="playlist/:id" element={<PlayList />} />
  <Route path="my-playlists" element={<UserPlaylist />} />
  <Route path="search" element={<Search />} />
  <Route path="mv/:id" element={<PlayVideoMusic />} />
</Route>
```

---

#### 4. Các component chính

##### 4.1. Header (Head.jsx)

Thanh điều hướng chứa logo, menu (Home, Search, My Playlists), nút đăng nhập/đăng ký hoặc avatar.

##### 4.2. Home (Home.jsx)

Hiển thị banner (`Slider.jsx`), danh sách bài hát nổi bật, nghệ sĩ, album. Dữ liệu load từ file JSON giả lập.

##### 4.3. Slider (Slider.jsx)

Component trượt ảnh/banner, có thể dùng CSS thuần hoặc thư viện Swiper.

##### 4.4. Login & Register (Login.jsx, Register.jsx)

Form đăng nhập/đăng ký với `react-hook-form`, xác thực cơ bản. Sau khi submit, lưu token vào `localStorage` thông qua `GetToken.jsx`.

##### 4.5. Search (Search.jsx)

Ô tìm kiếm lọc bài hát, nghệ sĩ, album từ mock data.

##### 4.6. PlayList & UserPlaylist (PlayList.jsx, UserPlaylist.jsx)

Xem chi tiết một playlist, quản lý danh sách playlist của người dùng (thêm, xóa).

##### 4.7. Music Player (MusicPlayer.jsx)

Thanh phát nhạc fixed bottom, sử dụng `PlayerContext` và thẻ `<audio>`, gồm các nút điều khiển cơ bản.

##### 4.8. MV (PlayVideoMusic.jsx)

Trang xem MV, nhúng `react-player`, hiển thị thông tin và MV liên quan.

---

#### 5. Kết quả

Sau khi hoàn thành, giao diện người dùng hoạt động đầy đủ với dữ liệu mock. Hình ảnh tham khảo:
Giao diện trang chủ
![Trang chủ với Slider và danh sách](/images/5-Workshop/5.3-S3-vpc/anhmh.png)
Giao diện trang album
![Album](/images/5-Workshop/5.3-S3-vpc/album.png)
Giao diện phát MV
![mv](/images/5-Workshop/5.3-S3-vpc/mv.png)
Giao diện playlist của user
![playlist](/images/5-Workshop/5.3-S3-vpc/playlist.png)
Giao diện đăng nhập
![playlist](/images/5-Workshop/5.3-S3-vpc/login.png)
Giao diện đăng ký 
![playlist](/images/5-Workshop/5.3-S3-vpc/dangky.png)