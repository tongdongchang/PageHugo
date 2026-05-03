---
title: "Các bước chuẩn bị"
date: 2026-05-01
weight: 2
chapter: false
pre: "<b> 4.2. </b>"
---


Trong phần này, chúng ta sẽ thiết lập môi trường phát triển tại máy cục bộ (Local Development) và cấu hình các công cụ cần thiết để tương tác với tài nguyên AWS.

### 1. Cài đặt môi trường lập trình

Dự án Website nghe nhạc của chúng ta sử dụng **Node.js** cho phần Frontend (React) và **Python** cho các kịch bản hỗ trợ/Backend.

#### 1.1. Cài đặt Node.js
* Tải và cài đặt phiên bản **Node.js LTS** (khuyên dùng bản 18.x hoặc 20.x).
* Kiểm tra sau khi cài đặt:
    ```bash
    node -v
    npm -v
    ```

#### 1.2. Cài đặt Python
* Tải và cài đặt **Python 3.9+**. Trong quá trình cài đặt, hãy nhớ tích chọn **"Add Python to PATH"**.
* Kiểm tra sau khi cài đặt:
    ```bash
    python --version
    # Hoặc trên macOS/Linux
    python3 --version
    ```

### 2. Cài đặt và cấu hình AWS CLI

AWS Command Line Interface (CLI) là công cụ giúp bạn quản lý các dịch vụ AWS bằng dòng lệnh.

#### 2.1. Cài đặt AWS CLI
* Tải bộ cài đặt phù hợp với hệ điều hành của bạn (Windows, macOS, hoặc Linux) từ trang chủ AWS.
* Kiểm tra phiên bản:
    ```bash
    aws --version
    ```

#### 2.2. Cấu hình tài khoản AWS (Free Tier)
Để máy tính của bạn có quyền thao tác với AWS, bạn cần cấu hình thông tin định danh (Credentials).

1.  Truy cập **IAM Console** > **Users** > Chọn người dùng của bạn.
2.  Tạo **Access Key** (loại CLI) và lưu lại `Access Key ID` và `Secret Access Key`.
3.  Chạy lệnh sau tại Terminal/Command Prompt:
    ```bash
    aws configure
    ```
4.  Nhập các thông tin:
    * **AWS Access Key ID**: [Của bạn]
    * **AWS Secret Access Key**: [Của bạn]
    * **Default region name**: `ap-southeast-1` (Singapore - hoặc khu vực bạn chọn)
    * **Default output format**: `json`



### 3. Tạo Key Pair cho EC2

Key Pair được sử dụng để kết nối SSH bảo mật vào máy chủ EC2 sau khi triển khai.

1.  Truy cập vào **Amazon EC2 Console**.
2.  Ở thanh điều hướng bên trái, chọn **Network & Security** > **Key Pairs**.
3.  Chọn **Create key pair**.
4.  Cấu hình:
    * **Name**: `MusicAppKeyPair`
    * **Key pair type**: `RSA`
    * **Private key file format**: `.pem` (cho OpenSSH) hoặc `.ppk` (cho PuTTY).
5.  Chọn **Create key pair** và lưu file về máy (Lưu ý: Bạn chỉ có thể tải file này một lần duy nhất).



### 4. Clone Source Code mẫu

Chúng ta sẽ sử dụng bộ mã nguồn đã được chuẩn bị sẵn bao gồm giao diện người dùng và cấu trúc thư mục triển khai.

1.  Mở Terminal và di chuyển đến thư mục bạn muốn lưu dự án.
2.  Sử dụng Git để lấy mã nguồn:
    ```bash
    git clone https://github.com/tongdongchang/code-aws.git
    cd code-aws
    ```
    
3.  Kiểm tra cấu trúc thư mục sơ bộ:
    * `/frontend`: Mã nguồn ReactJS.
    * `/backend`: API và Database schema.
    * `/scripts`: Các file hỗ trợ triển khai.

### 5. Kiểm tra quyền hạn tài khoản (AWS Free Tier)

Hãy đảm bảo tài khoản AWS của bạn đang trong chương trình **Free Tier** để tránh các chi phí phát sinh không mong muốn. Trong suốt workshop này, chúng ta sẽ ưu tiên sử dụng các cấu hình thuộc nhóm miễn phí (t2.micro, S3 Standard 5GB, v.v.).

{{% notice info %}}
Sau khi hoàn tất các bước trên, bạn đã sẵn sàng để bước sang phần tiếp theo: **Khởi tạo hạ tầng cơ bản trên AWS**.
{{% /notice %}}