---
title: "Proposal"
date: 2026-03-09
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Online Music Streaming Website  
## A Full‑stack Platform with React, Django, and AWS Infrastructure  

### 1. Executive Summary  
The music streaming website is developed within the **First Cloud Journey** programme to deliver a complete web application where users can listen to music, manage playlists, watch music videos, and search for artists/albums. The project uses React for the frontend and Django for the backend API, deployed on AWS services including S3, CloudFront, Route 53, and EC2. In addition to the user interface, the system includes a dedicated admin panel for managing songs, MVs, artists, albums, and users. The goal is to finish a real‑world product in **8 weeks**, helping the intern team to master full‑stack development and cloud deployment.

### 2. Problem Statement  
*Current situation*  
Building a complete music streaming website requires knowledge of both frontend and backend, as well as production deployment. Existing solutions are often complex, expensive, or do not allow deep customisation. The intern team needs a practical project to build their skills while staying within limited resources (AWS Free Tier and open‑source tools).

*Proposed solution*  
Build a music streaming website from scratch, using:
- **React** (Vite) to create both the user interface and the admin panel, supporting music playback, search, and playlist management.
- **Django REST Framework** to develop APIs for client and admin, with user authentication via JWT.
- **AWS** for deployment: S3 + CloudFront + Route 53 for the static frontend, EC2 for the Django backend.
The solution focuses on a simple, extensible architecture that is cost‑effective and suitable for learning/research environments.

*Benefits and Return on Investment (ROI)*  
- Students gain a real product for their reports and portfolios.
- They master the full‑stack development workflow and AWS deployment.
- Infrastructure cost is almost zero by leveraging the AWS Free Tier during the internship.
- The platform can be reused as a template for similar projects in the future.

### 3. Solution Architecture  
The whole system is divided into two main blocks:

- **Frontend**: A React Single Page Application built into static files, stored on S3 and distributed via CloudFront. A custom domain points to CloudFront through Route 53.
- **Backend**: Django runs on an EC2 virtual machine, handling API processing, authentication, and serving media files. APIs are protected by JWT, and the admin API requires staff privileges.

*AWS services used*
- **Amazon S3**: Hosts the static React frontend.
- **Amazon CloudFront**: CDN to accelerate and provide HTTPS for the frontend.
- **Amazon Route 53**: Manages the domain name and routes traffic to CloudFront.
- **Amazon EC2**: Virtual server running Django + Gunicorn + Nginx.
- *(Optional)* **Amazon RDS**: PostgreSQL database if scaling is needed.
- **AWS Certificate Manager**: Provides free SSL certificates for the domain.

*Component design*
- **User interface**: Home, Register/Login, Album, Playlist, Music Player, Search, MV watch pages.
- **Admin interface**: Manage songs, MVs, artists, albums, users, Dashboard.
- **Client API**: Endpoints for song/album/artist lists (with pagination, search), registration/login (JWT), personal playlist management.
- **Admin API**: Full CRUD on all resources, plus dashboard statistics.

### 4. Technical Implementation  
The project is carried out over an 8‑week roadmap:

| Week | Content | Main technologies |
|------|----------|-------------------|
| 1    | Get familiar with AWS, create Free Tier account, practice EC2, S3, CLI | AWS Console, CLI |
| 2    | Research project: music website requirements, React and Django technologies | React docs, Django docs |
| 3    | Build the complete user interface (React) | React, React Router, Context API, CSS |
| 4    | Build the admin panel (React) | React, Ant Design/Material UI |
| 5    | Develop client APIs (Django) | DRF, JWT, PostgreSQL/SQLite |
| 6    | Develop admin APIs (Django) | DRF, Permissions, File upload |
| 7    | Deploy to AWS: frontend to S3 + CloudFront + Route 53, backend to EC2 | S3, CloudFront, Route 53, EC2, Nginx, Gunicorn, SSL |
| 8    | Comprehensive testing, documentation, wrap‑up | Postman, Test cases, README |

*Technical requirements*
- **Frontend**: Node.js, Vite, React 18+, React Router, React Hook Form.
- **Backend**: Python 3.10+, Django 4.x, Django REST Framework, Simple JWT.
- **Deployment**: Ubuntu EC2, Nginx, Gunicorn, SSL (Let's Encrypt or ACM).
- **Database**: SQLite (development) or PostgreSQL (production).
- **Security**: HTTPS, JWT, CORS, Security Groups, Bucket Policies.

### 5. Roadmap & Milestones
- **Before internship**: Prior learning of basic React and Django (2–3 weeks).
- **Internship (8 weeks)**:
  - Week 1–2: AWS basics, technology research.
  - Week 3–4: Complete user and admin interfaces.
  - Week 5–6: Complete client and admin APIs.
  - Week 7: Production deployment.
  - Week 8: Testing, report, conclusion.
- **After deployment**: Can continue maintenance or extend features if needed.

### 6. Budget Estimation  
Thanks to the AWS Free Tier for the first 12 months, the expected cost is very low:

| Service              | Estimated monthly cost | Notes                                         |
|----------------------|------------------------|-----------------------------------------------|
| S3 (Standard)        | $0.02 USD              | Small storage (< 1 GB)                        |
| CloudFront           | $0.00 USD              | 1 TB free data transfer (Free Tier)           |
| Route 53             | $0.50 USD              | Hosted zone                                   |
| EC2 (t2.micro)       | $0.00 USD              | 750 hours/month free for 12 months            |
| **Total**            | **~$0.52 USD/month**   | ≈ $6.24 USD/12 months                         |

No hardware costs. Everything uses a personal AWS account and personal computer.

### 7. Risk Assessment  
*Risk matrix*
- **Schedule delay due to technical issues**: High impact, medium probability.
- **Unexpected cost overrun**: Low impact, low probability (Free Tier hard limits).
- **Limited AWS knowledge**: Medium impact, high probability.

*Mitigation strategies*
- Plan day‑by‑day with buffer in the final weeks.
- Monitor costs daily via AWS Budgets and restrict non‑Free Tier services.
- Learn AWS through the First Cloud Journey workshop and official documentation.

*Fallback plan*
- If EC2 fails, revert to local deployment to demonstrate features.
- Always back up source code on GitHub and periodically back up the database (if any).

### 8. Expected Outcomes  
*Skills acquired*
- Proficient in full‑stack web development with React and Django.
- Solid understanding of deploying applications on AWS (S3, CloudFront, Route 53, EC2).
- A tangible product to showcase competency.

*Deliverables*
- Frontend and backend source code (GitHub).
- Live website with complete user and admin functionality.
- Technical documentation, user manual, and internship report (8 weeks).