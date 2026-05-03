---
title : "Xây dựng API cho admin"
date : 2026-05-01
weight : 2
chapter : false
pre : " <b> 4.4.2. </b> "
---


### Mục tiêu

Xây dựng các REST API dành riêng cho trang quản trị (Admin Panel). Các API này cho phép thực hiện đầy đủ các thao tác CRUD trên tất cả tài nguyên: bài hát, MV, nghệ sĩ, album, người dùng. Ngoài ra còn cung cấp số liệu thống kê cho dashboard.

---

#### 1. Các endpoint admin đã có

Dựa vào file `views.py` và `urls.py`, hệ thống hiện đã có sẵn các API có thể dùng cho admin (chưa áp dụng phân quyền `is_staff`). Chúng ta sẽ sử dụng lại và bổ sung phân quyền.

##### 1.1. Quản lý nghệ sĩ (`/api/artist/`)

- **GET** `/api/artist/` – Lấy danh sách tất cả nghệ sĩ.
- **POST** `/api/artist/` – Tạo nghệ sĩ mới (`name`, `image_url`).
- **PUT** `/api/artist/<id>/` – Cập nhật nghệ sĩ (tên, ảnh).
- **DELETE** `/api/artist/<id>/` – Xóa nghệ sĩ (kèm xóa ảnh).

```python
# views.py - class AritistList(APIView)
def post(self, request):
    # Tạo nghệ sĩ
def put(self, request, id):
    # Sửa nghệ sĩ
def delete(self, request, id):
    # Xóa nghệ sĩ
### 1.2. Quản lý album (`/api/album/`)

* `GET /api/album/` – Danh sách album
* `POST /api/album/` – Tạo album mới
* `PUT /api/album/<id>/` – Cập nhật album
* `DELETE /api/album/<id>/` – Xóa album (kèm xóa ảnh)

Lớp **AlbumList** đã xử lý tất cả các method trên.

---

### 1.3. Quản lý bài hát (`/api/TrackChanging/`)

Endpoint dành cho admin (nên đổi tên rõ hơn nếu cần).

* `POST /api/TrackChanging/` – Thêm bài hát/MV mới
* `PUT /api/TrackChanging/<id>/` – Cập nhật bài hát
* `DELETE /api/TrackChanging/<id>/` – Xóa bài hát + file

```python id="py01"
# views.py
class TrackChanging(APIView):

    def post(self, request):
        # Tạo track mới (title, category, file, album, artists, is_premium,...)
        pass

    def put(self, request, id):
        # Cập nhật track
        pass

    def delete(self, request, id):
        # Xóa track + file
        pass
```

---

### 1.4. Quản lý playlist

Các API:

* `/api/playlist/`
* `/api/addtracktoplaylist/`
* `/api/EditPlaylist/`

Hiện gắn với user đăng nhập. Admin có thể mở rộng quyền để quản lý toàn bộ playlist.

---

### 2. Phân quyền admin

Sử dụng `IsAdminUser` để giới hạn quyền truy cập.

```python id="py02"
from rest_framework.permissions import IsAdminUser

class AritistList(APIView):
    permission_classes = [IsAdminUser]
```

---

### 3. API quản lý người dùng

```python id="py03"
class UserManagementView(APIView):
    permission_classes = [IsAdminUser]

    def get(self, request):
        users = CustomUser.objects.all()
        serializer = ProfileSerializer(users, many=True, context={'request': request})
        return Response(serializer.data)

    def put(self, request, id):
        user = get_object_or_404(CustomUser, id=id)

        user.is_active = request.data.get('is_active', user.is_active)
        user.is_staff = request.data.get('is_staff', user.is_staff)
        user.save()

        return Response({'message': 'Cập nhật thành công'})

    def delete(self, request, id):
        user = get_object_or_404(CustomUser, id=id)
        user.delete()

        return Response({'message': 'Xóa thành công'}, status=204)
```

Thêm URL:

```python id="py04"
path('admin/users/', views.UserManagementView.as_view(), name='admin-users')
```

---

### 4. Dashboard thống kê

```python id="py05"
class DashboardStatsView(APIView):
    permission_classes = [IsAdminUser]

    def get(self, request):
        data = {
            'total_tracks': Track.objects.count(),
            'total_artists': Artists.objects.count(),
            'total_albums': Album.objects.count(),
            'total_users': CustomUser.objects.count(),
            'total_playlists': Playlist.objects.count(),
        }
        return Response(data)
```

Endpoint:

```python id="py06"
path('admin/dashboard/', views.DashboardStatsView.as_view(), name='dashboard')
```

---

### 5. Tổng kết các endpoint admin

| Endpoint                   | Method      | Chức năng                |
| -------------------------- | ----------- | ------------------------ |
| `/api/artist/`             | GET, POST   | Danh sách & thêm nghệ sĩ |
| `/api/artist/<id>/`        | PUT, DELETE | Sửa, xóa nghệ sĩ         |
| `/api/album/`              | GET, POST   | Danh sách & thêm album   |
| `/api/album/<id>/`         | PUT, DELETE | Sửa, xóa album           |
| `/api/TrackChanging/`      | POST        | Thêm bài hát/MV          |
| `/api/TrackChanging/<id>/` | PUT, DELETE | Sửa, xóa bài hát         |
| `/api/admin/users/`        | GET         | Danh sách người dùng     |
| `/api/admin/users/<id>/`   | PUT, DELETE | Sửa/xóa người dùng       |
| `/api/admin/dashboard/`    | GET         | Dữ liệu thống kê         |

Tất cả endpoint yêu cầu `IsAdminUser` (`is_staff=True`).

---

### 6. Kết quả

Sau khi hoàn thành, hệ thống admin có thể:

* Quản lý toàn bộ tài nguyên âm nhạc
* Quản lý người dùng
* Hiển thị dashboard thống kê

Kết hợp với React Admin frontend để tạo giao diện trực quan.
