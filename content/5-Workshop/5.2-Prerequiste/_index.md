---
title: "Preparation Steps"
date: 2026-05-01
weight: 2
chapter: false
pre: "<b> 4.2. </b>"
---

In this section, we will set up the local development environment and configure the necessary tools to interact with AWS resources.

### 1. Development Environment Setup

Our Music Web Application project uses **Node.js** for the frontend (React) and **Python** for backend/support scripts.

#### 1.1. Install Node.js
- Download and install the **Node.js LTS** version (recommended: 18.x or 20.x).
- Verify the installation:
```bash
node -v
npm -v
```
####  1.2. Install Python
Download and install Python 3.9+. During installation, make sure to check "Add Python to PATH".
Verify the installation:
python --version
####  Or on macOS/Linux
python3 --version
### 2. Install and Configure AWS CLI

The AWS Command Line Interface (CLI) allows you to manage AWS services directly from the terminal.

 ####  2.1. Install AWS CLI
Download the installer suitable for your operating system (Windows, macOS, or Linux) from the AWS official website.
Verify installation:
aws --version
#### 2.2. Configure AWS Account (Free Tier)

To allow your machine to interact with AWS, you need to configure credentials.

Go to IAM Console → Users → Select your user.
Create an Access Key (CLI type) and save:
Access Key ID
Secret Access Key
Run the following command:
aws configure
Enter the required information:
AWS Access Key ID: [Your key]
AWS Secret Access Key: [Your key]
Default region name: ap-southeast-1 (Singapore or your preferred region)
Default output format: json
### 3. Create a Key Pair for EC2

A Key Pair is used to securely connect to your EC2 instance via SSH.

Go to Amazon EC2 Console.
In the left navigation panel, select Network & Security → Key Pairs.
Click Create key pair.
Configure:
Name: MusicAppKeyPair
Key pair type: RSA
Private key file format: .pem (for OpenSSH) or .ppk (for PuTTY)
Click Create key pair and download the file
⚠️ Note: This file can only be downloaded once.
### 4. Clone the Sample Source Code

We will use a prepared codebase that includes the frontend UI and deployment structure.

Open Terminal and navigate to your desired directory.
```
Clone the repository:
git clone https://github.com/tongdongchang/code-aws.git
cd code-aws
Project structure overview:
/frontend: ReactJS source code
/backend: API and database schema
/scripts: Deployment support scripts
```
### 5. Verify AWS Free Tier Eligibility

Ensure that your AWS account is within the Free Tier to avoid unexpected charges.
Throughout this workshop, we will prioritize free-tier resources (e.g., t2.micro, S3 Standard 5GB, etc.).

{{% notice info %}}
After completing these steps, you are ready to move on to the next section: Setting up the core infrastructure on AWS.
{{% /notice %}}