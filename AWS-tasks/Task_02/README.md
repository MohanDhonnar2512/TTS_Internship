# 🌐 Static Website Hosting on AWS S3

## 📌 Project Overview

This project demonstrates how to host a **static website** using **Amazon S3 (Simple Storage Service)**.  
Amazon S3 provides a highly scalable, durable, and cost-effective solution for hosting static content such as HTML, CSS, and JavaScript files.

This project is ideal for **Cloud / DevOps beginners** and suitable for **portfolio, internship, and academic submissions**.

---

## 🛠️ Technologies & Services Used

- **Amazon Web Services (AWS)**
  - Amazon S3 (Simple Storage Service)
- **Web Technologies**
  - HTML
  - CSS
- **Tools**
  - AWS Management Console
  - Web Browser

---

## 🏗️ Architecture



---

## 🎯 Project Objective

- Create an S3 bucket
- Upload static website files
- Configure public access
- Enable static website hosting
- Access the website using the S3 endpoint URL

---

## ✅ Prerequisites

Before starting, ensure you have:
- An **AWS account**
- A basic **index.html** file
- Basic understanding of **AWS S3**

---

## 🔄 Deployment Flow (Step-by-Step)

### Step 1: Create a New S3 Bucket
- Log in to the AWS Management Console
- Navigate to **S3 → Create bucket**
- Enter a **unique bucket name**
- Select the AWS region
- Create the bucket

---

### Step 2: Disable Block Public Access
- Open the created bucket
- Go to **Permissions**
- Disable **Block all public access**
- Save changes

---

### Step 3: Upload Website Files
- Navigate to the **Objects** tab
- Upload `index.html` file
- Make sure the file is uploaded successfully

---

### Step 4: Enable Static Website Hosting
- Go to **Properties**
- Scroll to **Static website hosting**
- Enable static website hosting
- Set:
  - Index document: `index.html`
- Save changes

---

### Step 5: Add Public Bucket Policy
Attach a bucket policy to allow public read access:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

### Step 6: Copy Website Endpoint URL
---

Go to Properties → Static website hosting

Copy the Bucket website endpoint URL
---

### Step 7: Access the Website
---
Open a web browser

Paste the S3 website endpoint URL

Your static website will be live 🎉
---