---
title : "Testing, Monitoring and Summary"
date : 2026-05-01
weight : 6
chapter : false
pre : " <b> 4.6. </b> "
---


### Objectives

After successfully deploying the music streaming website on AWS, we need to ensure the system works correctly, securely, and with acceptable performance. This section will guide you through:

- Functional testing of the entire user and admin flows.
- Assessment of basic security aspects.
- Preliminary performance measurement.
- Cleaning up AWS resources to avoid unnecessary costs after completion.

---

#### 1. Functional Testing

##### 1.1. Client Side (User)

Open a browser and navigate to the S3 static website address (or CloudFront if configured). Perform the following actions one by one:

| # | Task | Expected Outcome |
|---|------|------------------|
| 1 | Visit homepage | Banner, suggested songs, artists, albums are displayed. No console errors. |
| 2 | Register a new account | Form with `username`, `email`, `password`, `confirmPassword`. Successful registration redirects to login page. |
| 3 | Login | After login, header shows avatar/username instead of a Login button. Token is stored in localStorage. |
| 4 | View an album | Click an album – cover image, album info and song list are shown. |
| 5 | Play music | Click play on a song – Music Player bar appears, music plays, play/pause works. |
| 6 | Search | Enter a keyword in the search box; correct results are returned (songs, artists, albums). |
| 7 | Watch MV | Navigate to an MV; video plays using `react-player`. |
| 8 | Manage playlist | Create a new playlist, add songs, check “My Playlists” list. |

##### 1.2. Admin Side

Log in with an account that has `is_staff=True` (or use the default admin account if available). Access `/admin` (React Admin interface).

| # | Task | Expected Outcome |
|---|------|------------------|
| 1 | Dashboard | Displays statistics (songs, MVs, artists, users) – if the statistics API is integrated. |
| 2 | Manage songs | Add a new song (upload audio file), edit metadata, delete (with confirmation). |
| 3 | Manage MVs | Add an MV (video), edit, delete. |
| 4 | Manage albums | Create album, add/remove songs from album. |
| 5 | Manage artists | Add, edit, delete artists; upload avatar. |
| 6 | Manage users | View list, change role, lock/unlock account, delete. |

---

#### 2. Security Testing

##### 2.1. CORS and API Access

- Open the browser console and check requests from the frontend (S3) to the backend (EC2). There must be no CORS policy errors.
- If using `django-cors-headers` with `CORS_ALLOW_ALL_ORIGINS = True` (should only be used temporarily), requests will succeed. In production, restrict the origin list.

##### 2.2. Authentication and Authorization

- Clear the token (remove from localStorage) and try to access `/admin` – should be redirected to login.
- Call the create playlist API without a token (using Postman): server returns `401 Unauthorized`.
- Log in with a normal user account and try to call an admin API (e.g., delete a song): server returns `403 Forbidden`.

##### 2.3. Protecting AWS Resources

- S3 bucket policy only allows `s3:GetObject`; no upload/delete is permitted.
- EC2 security group only opens port 8000 (and port 22 limited to your IP). Optionally, you can scan quickly with `nmap` from outside.
- The IAM user `music-app-deployer` has only S3 and EC2 permissions, no IAM or RDS permissions.

---

#### 3. Performance Testing

##### 3.1. Frontend Evaluation

Use **Lighthouse** (in Chrome DevTools) to check Performance, Accessibility, Best Practices, SEO scores. Targets:
- Performance: score > 70.
- Optimize images: use WebP format, appropriate sizes.
- Homepage load time < 3 seconds.

##### 3.2. Backend Evaluation

Use **Postman** or **ab** (Apache Benchmark) to send 100 consecutive requests to the endpoint `/api/track/?category=audio`.
- Observe the average response time (should be under 500ms per request).
- Django `runserver` is not optimized for high concurrency, so this is only a basic check.

##### 3.3. Improvements (if time permits)

- Enable static caching on CloudFront (if used) with a long TTL.
- Apply gzip compression.
- Limit file upload sizes in the admin.

---

#### 4. Cleaning Up AWS Resources

After testing is complete and you no longer need the environment, delete the resources to avoid incurring charges.

##### 4.1. Terminate EC2 Instance

- Go to **EC2 console → Instances**. Select the `music-backend` instance. Click **Instance state → Terminate instance**. Confirm.

##### 4.2. Delete S3 Bucket

- Before deleting the bucket, you must remove all objects inside it.
- You can use the AWS CLI: `aws s3 rm s3://music-app-frontend --recursive`
- Then delete the bucket via the console or CLI: `aws s3 rb s3://music-app-frontend --force`

##### 4.3. Delete IAM User

- Go to **IAM → Users**. Select `music-app-deployer`. Delete its access keys, then click **Delete user**.

##### 4.4. Remove Other Resources (if any)

- Elastic IP: go to EC2 → Elastic IPs, release any unassociated IPs.
- CloudFront distribution: disable and delete.
- Route 53 hosted zone: delete all records, then delete the zone.

After cleanup, check the **Billing Dashboard** to confirm no resources are still running.

---

#### 5. Summary

Over the six parts of this workshop, you have:

- Built a complete music streaming website with React (client + admin).
- Created a backend API with Django REST Framework and JWT support.
- Deployed the application on AWS S3 and EC2 (albeit at a development level).
- Performed testing and ensured basic quality.
- Managed and cleaned up resources effectively.