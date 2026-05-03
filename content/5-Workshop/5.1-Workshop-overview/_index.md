---
title : "Introduction"
date : 2026-05-01
weight : 1
chapter : false
pre : " <b> 4.1. </b> "
---

#### Introduction to the Music Website Architecture

+ The system is split into two main blocks: **frontend** (React) and **backend** (Django), deployed on scalable, highly available AWS services.
+ The frontend is a Single Page Application hosted statically on **Amazon S3**, distributed globally via **CloudFront**, and accessed through a custom domain using **Route 53**.
+ The backend runs on an **EC2** virtual server, processes APIs and authenticates users via **JWT**; data is stored in **PostgreSQL** (can use RDS when scaling). The backend can be securely accessed from the frontend over HTTPS without traversing the public Internet.

#### Workshop overview
In this workshop, you will work with two main environments:
+ **Cloud Environment (AWS)**: where the entire system is deployed, including the S3 bucket, CloudFront distribution, Route 53 hosted zone, and EC2 instance running Django.
+ **Development Environment (Local)**: simulates a developer workstation, where you write React and Django code, run tests before pushing to AWS. An EC2 instance (in the Cloud environment) can be used as a remote build or test server, connected via SSH.

To minimise costs, the workshop leverages the **AWS Free Tier**, using only a single t2.micro EC2 instance and other free services. When planning for production, AWS recommends using multiple AZs and managed services (like RDS, Elastic Beanstalk) to ensure high availability.

![overview](/images/5-Workshop/5.1-Workshop-overview/flow.png)