---
title: "Week 5 Worklog"
date: 2026-04-06
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---


### Week 5 Objectives

* Build the Django backend to supply APIs for the client side (music streaming website).
* Complete APIs for: fetching, adding, editing, and deleting data for end users (excluding admin panel APIs).
* Ensure APIs include user authentication, authorization, search, and are ready to integrate with the React frontend.

### Detailed Task Schedule

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Monday | - Initialize Django project and the `music_api` app <br> - Configure Django REST Framework and JWT authentication <br> - Design models: Song, Artist, Album, Playlist, PlaylistSong, User (custom if needed) <br> - Create and run migrations | 04/06/2026 | 04/06/2026 | Django Docs, DRF Docs, Simple JWT |
| Tuesday | - Implement serializers for all models (Song, Artist, Album, Playlist, User) <br> - Create basic API views: list and detail for Song, Artist, Album (read-only for now) <br> - Set up URL routing for these endpoints | 04/07/2026 | 04/07/2026 | DRF Serializers, Generic Views |
| Wednesday | - Build registration (`/api/register/`) and login (`/api/token/`) endpoints using JWT <br> - Apply permissions: only authenticated users can manage their own playlists <br> - Develop Playlist APIs: list user playlists, create new, add/remove songs | 04/08/2026 | 04/08/2026 | DRF Authentication, ViewSets |
| Thursday | - Implement search API: filter songs by name, artist, album <br> - Add pagination and filtering for song and album lists <br> - Test all endpoints via Browsable API and Postman | 04/09/2026 | 04/09/2026 | DRF Filtering, django-filter |
| Friday | - Configure static/media file serving for audio (MEDIA_URL) <br> - Review code, optimize queries, handle errors <br> - Write Week 5 report | 04/10/2026 | 04/10/2026 | Django Static/Media, Compiled resources |

### Week 5 Outcomes

* Successfully built the Django backend with core APIs serving the music client:
  * Song API: listing, detail, search support, and pagination.
  * Artist API: listing, detail, including related albums/songs.
  * Album API: listing, album details, and contained songs.
  * Playlist API: personal playlist management for each user (create, edit, delete, add/remove songs).
* User authentication system works with JWT: registration, login, and protection of private endpoints.
* Each API enforces proper permissions (read-only for main content, write permissions only on the user’s own playlists).
* Search feature allows filtering songs by name, artist, or album, with suggestions and pagination.
* Media/static file serving is configured so the client can stream audio from the Django server (when applicable).
* All APIs have been tested with Postman and are ready to connect with the previously built React interfaces.