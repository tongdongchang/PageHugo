---
title: "Week 7 Worklog"
date: 2026-04-20
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---



### Week 7 Objectives

* Deploy the music streaming web application on AWS using three core services: S3, CloudFront, and Route 53 for the frontend; EC2 for the backend.
* Host the React interface on S3, distribute it globally via CloudFront, and manage a custom domain name with Route 53.
* Configure an EC2 virtual server to run the Django backend, serving APIs and static/media files.
* Ensure the entire system operates securely and stably in a production environment with HTTPS.

### Detailed Task Schedule

| Day       | Task                                                                                                                                                                                                                                                                                                    | Start Date | Completion Date | Reference Material                       |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|-----------------|------------------------------------------|
| Monday    | - Build the React production bundle with Vite, verify environment variables (API URL) <br> - Create an S3 bucket, enable static website hosting, configure bucket policy <br> - Upload the entire build folder (`dist`) to the bucket, confirm access via the default endpoint                           | 04/20/2026 | 04/20/2026      | AWS S3 Docs, Vite build guide            |
| Tuesday   | - Create a CloudFront distribution with the S3 bucket as origin, enable HTTP to HTTPS redirect <br> - Configure custom error response (403 → 200) to support SPA routing <br> - Request a public SSL certificate through AWS Certificate Manager, validate the domain <br> - Create a hosted zone on Route 53 (if not already existing), add an A record (Alias) pointing to the CloudFront distribution | 04/21/2026 | 04/21/2026      | AWS CloudFront, ACM, Route 53 docs       |
| Wednesday | - Launch an EC2 instance (Ubuntu), configure a security group to open ports 80/443 and SSH <br> - Install Python, virtualenv, clone the Django source code, set up the database (local PostgreSQL or RDS if required) <br> - Install Gunicorn, create a systemd service to run Django reliably                          | 04/22/2026 | 04/22/2026      | AWS EC2 Docs, Django deployment guide    |
| Thursday  | - Install Nginx as a reverse proxy for Gunicorn, configure serving of static/media files <br> - Set up HTTPS for the backend using Let’s Encrypt (certbot) or AWS Certificate Manager if using a Load Balancer <br> - Update CORS and `ALLOWED_HOSTS` in Django, test API over HTTPS                                     | 04/23/2026 | 04/23/2026      | Nginx, Let’s Encrypt, DRF CORS           |
| Friday    | - Update the React environment variable (API URL pointing to the backend domain), rebuild, re-upload to S3, and invalidate CloudFront cache if needed <br> - Test the complete flow: frontend (via domain) successfully calls the backend API, login, music playback, admin functions <br> - Write the Week 7 report, list issues and propose improvements | 04/24/2026 | 04/24/2026      | Compiled resources                       |

### Week 7 Outcomes

* The React frontend is stored on S3, delivered globally through CloudFront with low latency, HTTPS support, and a custom domain managed by Route 53.
* The Django backend runs on EC2:
  * Gunicorn + Nginx ensure stable API handling and static file serving.
  * The database (PostgreSQL or SQLite as appropriate) operates reliably.
  * HTTPS is enabled via Let’s Encrypt or ACM, securing data in transit.
* The entire website functions smoothly under a real domain, with frontend‑backend communication working without errors.
* Basic security measures are in place: the security group restricts ports, the bucket policy limits unnecessary public access, and HTTPS is enforced.
* Ready for the next stages such as monitoring (CloudWatch), CI/CD, automated backups, and cost optimization.