---
title : "Building the Client API"
date : 2026-05-01
weight : 1
chapter : false
pre : " <b> 4.4.1. </b> "
---

### Objectives

Provide REST APIs for the client side (end users) of the music streaming website. The system includes endpoints for fetching lists of songs, albums, artists, search, managing personal playlists, and JWT authentication.

---

### 1. Models

All models are defined in `models.py`. The main models are listed below (see the full file in the project):

- `Artists`: `name`, `image_url`
- `Album`: `title`, FK to `Artists`, `image_url`, `point`, `description`
- `Track`: `title`, FK to `Artists` and `Album`, `duration` (auto‑extracted from file), `category` (`audio`/`video`), `file`, `lyrics`, `is_Prenium`
- `CustomUser` (inherits `AbstractUser`): adds `is_premium`, `image_url`
- `Playlist`: `title`, FK to `CustomUser`, `image_url`, ManyToMany `song`

```python
# Example Track model
class Track(models.Model):
    title = models.CharField(max_length=100)
    artists = models.ForeignKey('Artists', on_delete=models.CASCADE, null=True, blank=True)
    album = models.ForeignKey('Album', on_delete=models.CASCADE, null=True, blank=True)
    duration = models.FloatField(blank=True, null=True)
    category = models.CharField(choices=[('audio', 'Audio'), ('video', 'Video')], max_length=50)
    file = models.FileField(upload_to=track_upload_path)
    # ...
    def save(self, *args, **kwargs):
        # automatically calculate duration
```
### 2. Serializers
The serializers.py file contains serializers that convert models to JSON and vice versa:

ArtistSerializer: returns name, image, total songs, total albums

AlbumSerializer: returns album info, track count

TrackSerializer: full fields, with absolute URLs for file and image

TrackASerializer: shortened version used in playlists and search

PlaylistSerializer: returns playlist together with list of songs

ProfileSerializer: user information
```
python
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
### 3. Client endpoint list
```
Endpoint	Method	Function
/api/register/	POST	Register new user
/api/token/	POST	Obtain access & refresh token (JWT)
/api/token/refresh/	POST	Refresh access token
/api/artist/	GET	List artists
/api/artist/<id>/	GET/PUT/DELETE	View, edit, delete artist (admin)
/api/track/	GET	List songs
/api/album/	GET	List albums
/api/album/<id>/	GET	Album detail
/api/trackalbum/	GET	Album + song list
/api/search/	GET	Quick search
/api/searchFull/	GET	Advanced search
/api/playlist/	GET, POST	List / create playlist
/api/playlist/?id=<id>	GET	Playlist detail
/api/addtracktoplaylist/	POST	Add track to playlist
/api/EditPlaylist/	POST	Edit playlist
/api/profile/	GET, POST	User profile
```
### 4. Details of some features
#### 4.1. Authentication & Registration
Register:
POST /api/register/ with username, email, password, confirmPassword

Login (JWT):
POST /api/token/ → returns access + refresh

Refresh token:
POST /api/token/refresh/

#### 4.2. Song API – Search
TrackList (GET /api/track/):

Filter by ?category=audio or video

If id + video → return MV detail

Ordered by -point

TrackListSearch (GET /api/search/):

Search by title, filter by category

Search (GET /api/searchFull/):

Search across songs, videos, albums

#### 4.3. Album
GET /api/album/: album list

GET /api/album/<id>/: album detail

POST/PUT/DELETE: for admin

ListTrackFromAlbum:

GET /api/trackalbum/?id=...

Returns album + song list

#### 4.4. Playlist
ListPlaylist (authentication required):

GET /api/playlist/: all playlists

GET /api/playlist/?id=...: playlist detail

POST /api/playlist/: create playlist

AddTrackToPlaylist:

POST /api/addtracktoplaylist/

EditPlaylist:

POST /api/EditPlaylist/

### 5. Security
Uses JWT for authentication

Personal endpoints require IsAuthenticated

Public APIs do not require a token

Registration is open to all users

### 6. Testing
After running the server, you can use:

DRF Browsable API

Postman

![api](/images/5-Workshop/5.4-S3-onprem/api.png)