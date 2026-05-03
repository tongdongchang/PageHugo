---
title: "Workshop"
date: 2026-05-01
weight: 5
chapter: false
pre: " <b> 4. </b> "
---


# Building and Deploying a Full‑stack Music Streaming Website on AWS

#### Overview

This workshop walks you step by step through building a complete **online music streaming website**, including the user interface (React), admin interface (React), backend API (Django), and deploying everything on AWS using services like S3, CloudFront, Route 53, and EC2.

Over the 8‑week internship, the workshop is split into six main parts, corresponding to each phase of the project. Each part includes detailed hands‑on instructions so you can recreate the system on your own.

#### Contents

1. [Workshop overview](5.1-workshop-overview/)  
   Introduction to objectives, system architecture, and the AWS services to be used.

2. [Environment and tools preparation](5.2-prerequiste/)  
   Install Node.js, Python, AWS CLI, configure an AWS Free Tier account, create a key pair, and clone the sample source code.

3. [Building the user and admin interfaces with React](5.3-s3-vpc/)  
   - Initialize a React project with Vite, set up the folder structure.  
   - Build pages: Home, Login/Register, Album, Playlist, Music Player, Search, MV.  
   - Build the Admin interface: manage songs, MVs, artists, albums, users.

4. [Developing the REST API with Django](5.4-s3-onprem/)  
   - Create a Django project, configure the database, DRF, and JWT.  
   - Client‑side APIs: songs, artists, albums, playlists, search, authentication.  
   - Admin APIs: full CRUD for all resources, dashboard statistics.

5. [Deploying the application to AWS](5.5-policy/)  
   - Put the frontend on S3, configure CloudFront and Route 53.  
   - Launch an EC2 instance, install Gunicorn + Nginx, set up HTTPS.  
   - Connect the frontend and backend.

6. [Testing, monitoring, and wrap‑up](5.6-cleanup/)  
   - Functional, security, and performance testing.  
   - Cleaning up AWS resources after completion.

#### Workshop notes

- Take advantage of the **AWS Free Tier** to avoid incurring costs.
- Always back up your source code to Git frequently.
- Each part can be completed independently in 1–2 sessions, fitting an internship schedule.

Start with the first part: [Workshop overview](5.1-workshop-overview/)