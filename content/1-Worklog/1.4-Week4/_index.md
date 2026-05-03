---
title: "Week 4 Worklog"
date: 2026-03-30
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---



### Week 4 Objectives

* Develop the Admin Panel interface for the music streaming website.
* Complete management features for: audio (songs), MVs, artists, albums, and users (add, edit, delete).
* Build an intuitive dashboard, ensuring smooth operations and ready for API integration.

### Detailed Task Schedule

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Create the Admin area in the React project (route `/admin`), layout with sidebar + main content <br> - Design the Audio management page: song list table, add/edit form (file upload, metadata), delete button <br> - Use mock data for Audio | 03/30/2026 | 03/30/2026 | React Router, Ant Design / Material UI docs |
| 3   | - Build the MV management page: display MV list, form for video upload/link, edit info, delete <br> - Integrate React Hook Form and state management similarly <br> - Mock data for MVs | 03/31/2026 | 03/31/2026 | React Hook Form, simulated upload API |
| 4   | - Develop Artist management: CRUD for name, bio, avatar, linked albums <br> - Album management: create album, add/remove songs, edit info, delete <br> - Reusable form and table components | 04/01/2026 | 04/01/2026 | Component reuse patterns |
| 5   | - Build User management page: user list, role change (admin/user), lock/unlock account, delete <br> - Create overview Dashboard: stats for songs, MVs, artists, users (mock) | 04/02/2026 | 04/02/2026 | Chart library (recharts), mock data |
| 6   | - Review the entire Admin interface, ensure validation, responsive design, error/success notifications <br> - Write Week 4 report and update team progress | 04/03/2026 | 04/03/2026 | Compiled resources |

### Week 4 Outcomes

* Completed the administration interface with all core data management functionalities.
* Audio management page: displays song list, supports add (simulated file upload), edit metadata, delete with confirmation.
* MV management page: similarly manages music videos, including link input or file selection, MV description, safe deletion.
* Artist management page: full CRUD, avatar upload, quick links to artist’s albums.
* Album management page: create new album, add/remove songs, edit album details, delete album.
* User management page: paginated user list, role modification, account locking, user deletion.
* Dashboard provides an overview with key statistics (mock data) in a clean visual layout.
* All pages include input validation, status feedback (loading, error, success), and basic responsive compatibility, ready to replace mock data with real APIs.