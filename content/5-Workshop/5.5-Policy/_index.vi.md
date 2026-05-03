---
title : "Triển khai ứng dụng lên AWS"
date : 2026-05-01
weight : 5
chapter : false
pre : " <b> 4.5. </b> "
---


### Mục tiêu

Đưa toàn bộ website nghe nhạc lên hạ tầng AWS theo cách đơn giản nhất:
- **Frontend React** được build thành tệp tĩnh và lưu trên **Amazon S3**, cho phép truy cập công khai qua Internet.
- **Backend Django** chạy trên một máy ảo **EC2** bằng lệnh `python manage.py runserver` (development server) để nhanh chóng kiểm thử.
- Quản lý quyền truy cập bằng một **IAM user** riêng, chỉ cấp đủ quyền cần thiết cho S3 và EC2.



---

#### 1. Tạo IAM user để phân quyền

Nhằm tránh sử dụng tài khoản root, chúng ta sẽ tạo một IAM user chuyên dùng cho việc deploy, chỉ cấp quyền hạn chế.

1. Vào **AWS Management Console → IAM → Users → Create user**.
2. Đặt tên user (ví dụ `music-app-deployer`), chọn **Provide user access to the AWS Management Console** nếu muốn dùng console, và **Access key - Programmatic access** để dùng CLI.
3. Ở bước **Set permissions**, chọn **Attach policies directly**, tìm và gắn các policy sau:
   - `AmazonS3FullAccess`
   - `AmazonEC2FullAccess`
4. Hoàn tất, tải file `.csv` chứa Access Key ID và Secret Access Key.

Bạn sẽ dùng thông tin này để cấu hình AWS CLI trên máy cá nhân (hoặc EC2) bằng `aws configure`.
![IAM](/images/5-Workshop/5.5-Policy/iam.png)

---

#### 2. Triển khai frontend lên S3

##### 2.1. Build dự án React

Trên máy cá nhân, trong thư mục `frontend`:

```bash
npm run build
Lệnh này tạo thư mục dist (hoặc build) chứa các tệp tĩnh.
```
##### 2.2. Tạo S3 bucket và kích hoạt web hosting
Vào S3 console, chọn Create bucket.

Đặt tên bucket (ví dụ music-app-frontend).

Chọn region us-east-1.

Bỏ chọn Block all public access (xác nhận rằng bạn muốn bucket được công khai).

Nhấn Create.

Vào bucket vừa tạo, chuyển đến tab Properties.

Cuối trang, kích hoạt Static website hosting.

Index document: index.html

Error document: index.html (để React Router xử lý lỗi).

Tab Permissions → Bucket policy, dán policy sau:
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
Ảnh: Cấu hình bucket policy cho phép public đọc file.

##### 2.3. Upload file lên bucket
Có thể dùng AWS CLI hoặc giao diện web:
```
bash
aws s3 cp dist/ s3://music-app-frontend/ --recursive
```
Sau khi upload, truy cập vào endpoint được cung cấp trong phần Static website hosting (dạng http://music-app-frontend.s3-website-us-east-1.amazonaws.com) để thấy giao diện React chạy.

Ảnh: Trang chủ React hiển thị từ S3 bucket.
![React](/images/5-Workshop/5.5-Policy/s3.png)
#### 3. Triển khai backend lên EC2
##### 3.1. Tạo EC2 instance
Vào EC2 console, chọn Launch Instance.

Name: music-backend

AMI: Ubuntu 22.04 LTS (hoặc Amazon Linux 2)

Instance type: t2.micro (free tier)

Key pair: chọn key đã tạo (ví dụ music-app-key)

Network settings: tạo mới một security group, mở các cổng:

SSH (22) – cho phép truy cập từ IP của bạn.

HTTP (80) – tùy chọn nếu muốn truy cập qua cổng 80.

Custom TCP (8000) – cho phép kết nối đến Django runserver (bạn cũng có thể giới hạn chỉ cho IP của frontend S3 nếu cần).

Nhấn Launch instance.

Ảnh: Cấu hình Security Group với cổng 22, 80, 8000.

##### 3.2. Kết nối và cài đặt môi trường
Sau khi instance chạy, kết nối SSH:

bash
ssh -i music-app-key.pem ubuntu@<public-ip>
Cập nhật hệ thống và cài Python, pip, virtualenv:

bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip python3-venv -y
python3 -m venv venv
source venv/bin/activate
##### 3.3. Đưa mã nguồn lên EC2
Bạn có thể clone từ GitHub trực tiếp trên EC2 (nếu repo public) hoặc copy thư mục backend từ máy cá nhân bằng scp:

bash
##### từ máy cá nhân
scp -i music-app-key.pem -r backend/ ubuntu@<public-ip>:~/backend/
Sau đó, trên EC2:
```
bash
cd backend
pip install -r requirements.txt
```
Cần nhớ cài thêm django-cors-headers và thêm vào INSTALLED_APPS + Middleware trong settings.py để frontend gọi API không bị chặn CORS.

Thiết lập CORS (trong settings.py):

python
INSTALLED_APPS = [
    ...,
    'corsheaders',
]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',
    ...
]

CORS_ALLOW_ALL_ORIGINS = True   # chỉ dùng khi dev
##### 3.4. Chạy Django
Chỉnh sửa ALLOWED_HOSTS trong settings.py để chấp nhận IP công cộng hoặc tên miền:

python
ALLOWED_HOSTS = ['*']   # tạm thời mở rộng, sau này nên giới hạn
Chạy migration:
```
bash
python manage.py migrate
Khởi động server:
```
bash
python manage.py runserver 0.0.0.0:8000
Ảnh: Terminal hiển thị Django runserver đang chạy trên EC2.
![EC2](/images/5-Workshop/5.5-Policy/ec2.png)
### 4. Kết nối frontend và backend
Trong source React, tạo file .env hoặc sửa trực tiếp biến API URL (ví dụ trong src/api.js) trỏ đến địa chỉ IP thực của EC2:

text
VITE_API_URL=http://<ec2-public-ip>:8000/api/
Build lại frontend và upload lại S3.

Sau đó, mở trình duyệt với địa chỉ S3 static website, thử đăng ký, đăng nhập, nghe nhạc. Các yêu cầu từ frontend sẽ gửi thẳng đến EC2 qua cổng 8000.

### 5. Kiểm tra và lưu ý
Đảm bảo security group cho EC2 chỉ mở cổng 8000 từ 0.0.0.0/0 (hoặc từ S3 nếu bạn biết dải IP của CloudFront/S3). Với mục đích thực tập, mở rộng cũng chấp nhận được.

Nên tắt instance khi không sử dụng để tiết kiệm chi phí.

Không sử dụng runserver lâu dài; đây chỉ là phương án tạm thời giúp bạn nhanh chóng có một bản demo.