---
title : "Deploying the Application on AWS"
date : 2026-05-01
weight : 5
chapter : false
pre : " <b> 4.5. </b> "
---



### Objectives

Deploy the entire music streaming website on AWS infrastructure in the simplest way possible:
- **React Frontend** is built into static files and stored on **Amazon S3**, allowing public access over the Internet.
- **Django Backend** runs on an **EC2** virtual machine using the command `python manage.py runserver` (development server) for quick testing.
- Manage access permissions with a dedicated **IAM user**, granting only the necessary rights for S3 and EC2.

---

#### 1. Create an IAM user for permissions

To avoid using the root account, we will create a dedicated IAM user for deployment with limited permissions.

1. Go to **AWS Management Console → IAM → Users → Create user**.
2. Name the user (e.g., `music-app-deployer`), select **Provide user access to the AWS Management Console** if you want console access, and **Access key - Programmatic access** for CLI use.
3. In the **Set permissions** step, choose **Attach policies directly**, find and attach the following policies:
   - `AmazonS3FullAccess`
   - `AmazonEC2FullAccess`
4. Complete the process and download the `.csv` file containing the Access Key ID and Secret Access Key.

You will use these credentials to configure the AWS CLI on your local machine (or EC2) via `aws configure`.
![IAM](/images/5-Workshop/5.5-Policy/iam.png)

---

#### 2. Deploy the frontend to S3

##### 2.1. Build the React project

On your local machine, inside the `frontend` directory:

```bash
npm run build
This command creates a dist (or build) folder containing the static files.
```

##### 2.2. Create an S3 bucket and enable web hosting
Go to the S3 console, click Create bucket.

Name the bucket (e.g., music-app-frontend).

Select the region us-east-1.

Uncheck Block all public access (acknowledge that you want the bucket to be public).

Click Create.

Enter the newly created bucket, go to the Properties tab.

At the bottom of the page, enable Static website hosting.

Index document: index.html

Error document: index.html (to let React Router handle errors).

Go to the Permissions tab → Bucket policy, and paste the following policy:

```
json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::music-app-frontend/*"
    }
  ]
}
```

Image: Bucket policy configured to allow public read access to files.


##### 2.3. Upload files to the bucket
You can use the AWS CLI or the web interface:

bash
aws s3 cp dist/ s3://music-app-frontend/ --recursive
After uploading, visit the endpoint provided in the Static website hosting section (e.g., http://www.myprojectawsfcaj.live.s3-website-ap-southeast-1.amazonaws.com) to see the React interface running.

![s3](/images/5-Workshop/5.5-Policy/s3.png)
Image: React homepage displayed from the S3 bucket.


#### 3. Deploy the backend to EC2

##### 3.1. Create an EC2 instance
Go to the EC2 console, click Launch Instance.

Configure:

Name: music-backend

AMI: Ubuntu 22.04 LTS (or Amazon Linux 2)

Instance type: t2.micro (free tier)

Key pair: select the key you created (e.g., music-app-key)

Network settings: create a new security group and open the following ports:

SSH (22) – allow access from your IP.

HTTP (80) – optional if you want to access via port 80.

Custom TCP (8000) – to allow connections to the Django runserver (you can also restrict it to the S3 frontend IP if needed).

Click Launch instance.

Image: Security Group configuration with ports 22, 80, 8000.


##### 3.2. Connect and set up the environment
After the instance is running, connect via SSH:

bash
ssh -i music-app-key.pem ubuntu@<public-ip>
Update the system and install Python, pip, virtualenv:

bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip python3-venv -y
python3 -m venv venv
source venv/bin/activate

##### 3.3. Transfer the source code to EC2
You can clone directly from GitHub on the EC2 instance (if the repo is public) or copy the backend folder from your local machine using scp:

bash
## from your local machine
scp -i music-app-key.pem -r backend/ ubuntu@<public-ip>:~/backend/
Then, on EC2:

bash
cd backend
pip install -r requirements.txt
Remember to install django-cors-headers and add it to INSTALLED_APPS and MIDDLEWARE in settings.py so the frontend can call the API without CORS issues.

CORS configuration (in settings.py):
```
python
INSTALLED_APPS = [
    ...,
    'corsheaders',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    ...
]
```
CORS_ALLOW_ALL_ORIGINS = True   # only for development

##### 3.4. Run Django
Edit ALLOWED_HOSTS in settings.py to accept the public IP or domain:

python
ALLOWED_HOSTS = ['*']   # temporarily open; restrict later
Run migrations:

bash
python manage.py migrate
Start the server:

bash
python manage.py runserver 0.0.0.0:8000
![ec2](/images/5-Workshop/5.5-Policy/ec2.png)
Image: Terminal showing Django runserver running on EC2.


#### 4. Connect frontend and backend
In the React source code, create a .env file or directly modify the API URL variable (e.g., in src/api.js) to point to the actual IP address of the EC2 instance:

text
VITE_API_URL=http://<ec2-public-ip>:8000/api/
Rebuild the frontend and upload it to S3 again.

Then, open a browser with the S3 static website address and test registration, login, music playback. Requests from the frontend will be sent directly to EC2 on port 8000.


#### 5. Testing and notes
Ensure the EC2 security group only opens port 8000 from 0.0.0.0/0 (or from S3 if you know the IP range of CloudFront/S3). For internship purposes, a broader opening is acceptable.

Shut down the instance when not in use to save costs.
