---
title: "Week 6 Worklog"
date: 2026-04-13
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---


### Week 6 Objectives

* Develop a dedicated API system for the Admin Panel of the music streaming web application.
* Complete CRUD endpoints for managing audio (songs), music videos (MVs), artists, albums, and users.
* Build statistical APIs to support the admin dashboard overview.
* Implement strict authentication and authorization mechanisms for admin access.

### Detailed Weekly Schedule

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2 | - Create a separate `admin_api` app in the Django project to isolate admin functionalities from client APIs <br> - Configure admin access control: only users with `is_staff=True` are authorized <br> - Develop Audio (Song) management APIs: list (with pagination), create (file upload), update, delete | 04/13/2026 | 04/13/2026 | DRF Permissions, Django File Upload |
| 3 | - Develop MV management APIs: full CRUD operations with support for video upload or external URL input <br> - Implement file validation (format, size) for uploads <br> - Test endpoints using Postman | 04/14/2026 | 04/14/2026 | DRF FileUploadParser, Validation |
| 4 | - Build Artist management APIs: CRUD operations, avatar upload, and album relationship handling <br> - Build Album management APIs: CRUD, add/remove songs, update cover images | 04/15/2026 | 04/15/2026 | Nested Relationships, DRF Viewsets |
| 5 | - Develop User management APIs: listing (with search/filter), role updates, account locking/unlocking, deletion <br> - Implement Dashboard statistics APIs: total counts (songs, MVs, artists, users, playlists), latest songs, etc. | 04/16/2026 | 04/16/2026 | DRF Filtering, Aggregation |
| 6 | - Conduct security review: verify all permissions to prevent privilege escalation <br> - Write API documentation (Swagger/Redoc if applicable) <br> - Summarize Week 6 and prepare report | 04/17/2026 | 04/17/2026 | DRF Docs, drf-yasg, Documentation |

### Week 6 Achievements

* Successfully completed the full set of APIs for the admin panel, ready for integration with the React-based admin interface.
* Implemented core API modules:
  * **Audio Admin API**: full song management (create, update, delete, MP3 upload) with pagination and filtering support.
  * **MV Admin API**: music video management with upload/link support, format validation, and status updates.
  * **Artist Admin API**: CRUD operations for artists, image uploads, and efficient album associations ensuring data consistency.
  * **Album Admin API**: full album management, including song organization and cover image updates.
  * **User Admin API**: system-wide user management, role assignment, and account control (lock/unlock).
* Developed Dashboard APIs providing real-time statistical data for the admin overview page.
* Implemented a secure admin authorization system: only users with `staff` privileges can access admin endpoints, preventing unauthorized access.
* Ensured all endpoints include proper input validation, clear error handling, and follow RESTful standards.
* All APIs were thoroughly tested using Postman and are ready for integration with the Admin React interface developed in Week 4.