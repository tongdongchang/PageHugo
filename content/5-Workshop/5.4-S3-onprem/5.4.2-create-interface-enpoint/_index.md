---
title : "Building the Admin API"
date : 2026-05-01
weight : 2
chapter : false
pre : " <b> 4.4.2. </b> "
---


### Objectives

Build dedicated REST APIs for the Admin Panel. These APIs enable full CRUD operations on all resources: songs, MVs, artists, albums, and users. They also provide statistical data for the dashboard.

---

### 1. Existing Admin Endpoints

Based on the `views.py` and `urls.py` files, several APIs are already available for admin tasks (currently without `is_staff` permission enforcement). We will reuse them and add appropriate permissions.

#### 1.1. Artist Management (`/api/artist/`)

- **GET** `/api/artist/` – Retrieve all artists.
- **POST** `/api/artist/` – Create a new artist (`name`, `image_url`).
- **PUT** `/api/artist/<id>/` – Update an artist (name, image).
- **DELETE** `/api/artist/<id>/` – Delete an artist (along with its image).

```python
# views.py - class AritistList(APIView)
def post(self, request):
    # Create artist
def put(self, request, id):
    # Update artist
def delete(self, request, id):
    # Delete artist
``` 

#### 1.2. Album Management (/api/album/)
GET /api/album/ – List of albums.

POST /api/album/ – Create a new album.

PUT /api/album/<id>/ – Update an album.

DELETE /api/album/<id>/ – Delete an album (including its cover image).

The AlbumList class already handles all these methods.

#### 1.3. Track Management (/api/TrackChanging/)
Endpoint dedicated to admin (can be renamed for clarity).

POST /api/TrackChanging/ – Add a new song/MV.

PUT /api/TrackChanging/<id>/ – Update a song.

DELETE /api/TrackChanging/<id>/ – Delete a song along with its file.

```
python
# views.py
class TrackChanging(APIView):

    def post(self, request):
        # Create new track (title, category, file, album, artists, is_premium,...)
        pass

    def put(self, request, id):
        # Update track
        pass

    def delete(self, request, id):
        # Delete track + file
        pass
``` 

#### 1.4. Playlist Management
Existing playlist endpoints (/api/playlist/, /api/addtracktoplaylist/, /api/EditPlaylist/) are linked to the authenticated user. Admin can extend permissions to manage any playlist.

### 2. Admin Permissions
```
Use IsAdminUser to restrict access to admin endpoints.

python
from rest_framework.permissions import IsAdminUser

class AritistList(APIView):
    permission_classes = [IsAdminUser]
```
### 3. User Management API
```
python
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

        return Response({'message': 'Updated successfully'})

    def delete(self, request, id):
        user = get_object_or_404(CustomUser, id=id)
        user.delete()

        return Response({'message': 'Deleted successfully'}, status=204)
Add URL:

python
path('admin/users/', views.UserManagementView.as_view(), name='admin-users')
``` 

### 4. Dashboard Statistics
```
python
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
Endpoint:
```
```
python
path('admin/dashboard/', views.DashboardStatsView.as_view(), name='dashboard')
```

### 5. Summary of Admin Endpoints
```
Endpoint	Method	Function
/api/artist/	GET, POST	List & create artists
/api/artist/<id>/	PUT, DELETE	Edit, delete artist
/api/album/	GET, POST	List & create albums
/api/album/<id>/	PUT, DELETE	Edit, delete album
/api/TrackChanging/	POST	Add song/MV
/api/TrackChanging/<id>/	PUT, DELETE	Edit, delete song
/api/admin/users/	GET	List users
/api/admin/users/<id>/	PUT, DELETE	Edit / delete user
/api/admin/dashboard/	GET	Dashboard statistics
All endpoints require IsAdminUser (is_staff=True).
```
### 6. Outcome
After completion, the admin system can:

Manage all music resources

Manage users

Display dashboard statistics

Combine with the React Admin frontend to build an intuitive management interface.