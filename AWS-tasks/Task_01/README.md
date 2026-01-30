# 🚀 Website Deployment on AWS EC2 using Nginx

## 📌 Project Overview

This project demonstrates how to deploy a static website on an **AWS EC2 Ubuntu instance** using the **Nginx web server**.  
It covers the complete flow from launching an EC2 instance to accessing the website through a public IP address.

This project is suitable for **Cloud / DevOps beginners** and can be used as a **portfolio or internship project**.

---

## 🛠️ Technologies & Services Used

- **Amazon Web Services (AWS)**
  - EC2 (Elastic Compute Cloud)
  - VPC
- **Operating System**
  - Ubuntu Linux
- **Web Server**
  - Nginx
- **Tools**
  - PuTTY (for SSH connection)
  - Browser (to access the website)

---


## Architecture

![Uploading image.png…]()

---

## ✅ Prerequisites

Before starting, ensure you have:
- An **AWS account**
- **PuTTY** installed on your local system
- A basic understanding of **Linux commands**
- An **EC2 key pair (.pem / .ppk)** file

---

## 🔄 Deployment Flow (Step-by-Step)

### Step 1: Launch an Ubuntu EC2 Instance
- Log in to AWS Console
- Launch a new **Ubuntu EC2 instance**
- Choose instance type (e.g., `t2.micro`)
- Create or select an existing key pair

---

### Step 2: Configure Security Group
Allow the following inbound rules:
- **SSH** – Port `22` (for remote access)
- **HTTP** – Port `80` (for website access)

---

### Step 3: Connect to EC2 using PuTTY
- Convert `.pem` to `.ppk` if required
- Use the **public IP** of the EC2 instance
- Login user: `ubuntu`

---

### Step 4: Update System Packages

sudo apt update && sudo apt upgrade -y

### Step 5: Install Nginx Web Server
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
```
### Step 6: Start and Enable Nginx
```bash

sudo systemctl start nginx
sudo systemctl enable nginx

```

### Step 7: Edit Website Content
Navigate to the default web directory:
```bash
cd /var/www/html
Edit the website file:
sudo nano index.html
Add your custom HTML content and save the file.
```

### Step 8: Restart Nginx Service
```bash
sudo systemctl restart nginx
```

### Step 9: Access the Website
- Open a web browser
- Enter the EC2 Public IP Address
- Your website should be live 🎉
---
