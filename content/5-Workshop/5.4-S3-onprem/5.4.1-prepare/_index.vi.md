---
title : "Xây dựng API cho client"
date : 2026-05-01
weight : 1
chapter : false
pre : " <b> 4.4.1. </b> "
---



### Mục tiêu

Cung cấp REST API cho phía client (người dùng cuối) của website nghe nhạc. Hệ thống bao gồm các endpoint lấy danh sách bài hát, album, nghệ sĩ, tìm kiếm, quản lý playlist cá nhân và xác thực JWT.

---

#### 1. Models

Toàn bộ model được định nghĩa trong `models.py`. Dưới đây là các model chính (xem file đầy đủ trong dự án):

- `Artists`: `name`, `image_url`
- `Album`: `title`, FK đến `Artists`, `image_url`, `point`, `description`
- `Track`: `title`, FK đến `Artists` và `Album`, `duration` (tự động lấy từ file), `category` (`audio`/`video`), `file`, `lyrics`, `is_Prenium`
- `CustomUser` (kế thừa `AbstractUser`): thêm `is_premium`, `image_url`
- `Playlist`: `title`, FK đến `CustomUser`, `image_url`, ManyToMany `song`

```python
# Ví dụ model Track
class Track(models.Model):
    title = models.CharField(max_length=100)
    artists = models.ForeignKey('Artists', on_delete=models.CASCADE, null=True, blank=True)
    album = models.ForeignKey('Album', on_delete=models.CASCADE, null=True, blank=True)
    duration = models.FloatField(blank=True, null=True)
    category = models.CharField(choices=[('audio', 'Audio'), ('video', 'Video')], max_length=50)
    file = models.FileField(upload_to=track_upload_path)
    # ...
    def save(self, *args, **kwargs):
        # tự động tính duration
### 2. Serializers

File `serializers.py` chứa các serializer chuyển đổi model thành JSON và ngược lại:

* **ArtistSerializer**: trả tên, ảnh, tổng bài hát, tổng album
* **AlbumSerializer**: trả thông tin album, số lượng bài hát
* **TrackSerializer**: đầy đủ các trường, kèm URL tuyệt đối cho file và ảnh
* **TrackASerializer**: phiên bản rút gọn dùng trong playlist và tìm kiếm
* **PlaylistSerializer**: trả playlist cùng danh sách bài hát
* **ProfileSerializer**: thông tin user

```python
class TrackSerializer(serializers.ModelSerializer):
    image_url = serializers.SerializerMethodField()
    file = serializers.SerializerMethodField()
    artists = serializers.CharField(source='artists.name', allow_null=True)
    # ...

class PlaylistSerializer(serializers.ModelSerializer):
    song = TrackASerializer(many=True)
    users = serializers.CharField(source='users.username')
    # ...
```

---

### 3. Danh sách endpoint client

| Endpoint                   | Phương thức    | Chức năng                        |
| -------------------------- | -------------- | -------------------------------- |
| `/api/register/`           | POST           | Đăng ký người dùng mới           |
| `/api/token/`              | POST           | Lấy access & refresh token (JWT) |
| `/api/token/refresh/`      | POST           | Làm mới access token             |
| `/api/artist/`             | GET            | Danh sách nghệ sĩ                |
| `/api/artist/<id>/`        | GET/PUT/DELETE | Xem, sửa, xoá nghệ sĩ (admin)    |
| `/api/track/`              | GET            | Danh sách bài hát                |
| `/api/album/`              | GET            | Danh sách album                  |
| `/api/album/<id>/`         | GET            | Chi tiết album                   |
| `/api/trackalbum/`         | GET            | Album + danh sách bài hát        |
| `/api/search/`             | GET            | Tìm kiếm nhanh                   |
| `/api/searchFull/`         | GET            | Tìm kiếm nâng cao                |
| `/api/playlist/`           | GET, POST      | Danh sách/tạo playlist           |
| `/api/playlist/?id=<id>`   | GET            | Chi tiết playlist                |
| `/api/addtracktoplaylist/` | POST           | Thêm bài hát vào playlist        |
| `/api/EditPlaylist/`       | POST           | Sửa playlist                     |
| `/api/profile/`            | GET, POST      | Hồ sơ người dùng                 |

---

### 4. Chi tiết một số chức năng

#### 4.1. Xác thực & đăng ký

* **Đăng ký**:
  `POST /api/register/` với `username`, `email`, `password`, `confirmPassword`

* **Đăng nhập (JWT)**:
  `POST /api/token/` → trả access + refresh

* **Refresh token**:
  `POST /api/token/refresh/`

---

#### 4.2. API bài hát – tìm kiếm

**TrackList** (`GET /api/track/`):

* Lọc theo `?category=audio` hoặc `video`
* Nếu có `id` + `video` → trả chi tiết MV
* Sắp xếp theo `-point`

**TrackListSearch** (`GET /api/search/`):

* Tìm theo `title`, lọc theo `category`

**Search** (`GET /api/searchFull/`):

* Tìm trong bài hát, video, album

---

#### 4.3. Album

* `GET /api/album/`: danh sách album
* `GET /api/album/<id>/`: chi tiết album
* `POST/PUT/DELETE`: dành cho admin

**ListTrackFromAlbum**:

* `GET /api/trackalbum/?id=...`
* Trả album + danh sách bài hát

---

#### 4.4. Playlist

**ListPlaylist** (cần đăng nhập):

* `GET /api/playlist/`: tất cả playlist
* `GET /api/playlist/?id=...`: chi tiết playlist
* `POST /api/playlist/`: tạo playlist

**AddTrackToPlaylist**:

* `POST /api/addtracktoplaylist/`

**EditPlaylist**:

* `POST /api/EditPlaylist/`

---

### 5. Bảo mật

* Sử dụng **JWT** cho xác thực
* Endpoint cá nhân yêu cầu `IsAuthenticated`
* API công khai không cần token
* Đăng ký mở cho tất cả người dùng

---

### 6. Kiểm tra

Sau khi chạy server, bạn có thể dùng:

* Browsable API của DRF
* Postman

![Browsable API](/images/5-Workshop/5.4-S3-onprem/api.png)
