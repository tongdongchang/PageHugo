---
title : "Developing REST API with Django"
date : 2026-05-01
weight : 4
chapter : false
pre : " <b> 4.4. </b> "
---



### Overview

This section guides you through building the entire backend API for the music streaming website using Django and Django REST Framework. The API system is divided into two main groups:

- **Client-side API** – serves the user interface: retrieve song, album, artist lists, search, register/login with JWT, manage personal playlists.
- **Admin API** – serves the admin interface: add, edit, delete songs, MVs, albums, artists, users; provide statistics for the dashboard.

The backend is built on Django 4.x, uses SQLite during development (can switch to PostgreSQL for production deployment), and is secured with JWT.

#### Contents

1. [Building the client API](5.4.1-prepare/) – Models, Serializers, Views, Endpoints for end users.
2. [Building the admin API](5.4.2-create-interface-enpoint/) – CRUD endpoints for resources and dashboard statistics.

After completing both parts, you will have a backend ready to serve data to the entire React interface built earlier.