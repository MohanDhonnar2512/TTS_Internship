# ⚖️ AWS Application Load Balancer with Multiple EC2 Instances

## 📌 Project Overview

This project demonstrates how to implement **Application Load Balancing (ALB)** on AWS to distribute incoming HTTP traffic across **multiple EC2 instances** running Nginx.

The setup improves **availability, scalability, and fault tolerance** by ensuring traffic is evenly distributed and continues to function even if one instance fails.

This project is ideal for learning **production-grade cloud architecture fundamentals**.

---

## 🛠️ Technologies & Services Used

- **Amazon Web Services (AWS)**
  - EC2 (Elastic Compute Cloud)
  - Application Load Balancer (ALB)
  - Target Groups
  - Security Groups
- **Operating System**
  - Ubuntu Linux
- **Web Server**
  - Nginx
- **Tools**
  - AWS Management Console
  - Web Browser

---

## 🏗️ Architecture


---

## 🎯 Project Objectives

- Launch multiple EC2 backend servers
- Configure automatic Nginx setup using User Data
- Create Target Group
- Configure Application Load Balancer
- Distribute traffic evenly
- Validate high availability

---

## ✅ Prerequisites

- AWS Account
- Basic Linux knowledge
- Understanding of EC2 and networking
- Web browser

---

## 🔄 Step-by-Step Implementation

---

### Step 1: Launch Three EC2 Instances

- Launch **3 Ubuntu EC2 instances**
- Place in public subnets
- Attach EC2 security group
- Allow HTTP and SSH

These instances act as backend servers.

---

### Step 2: Configure EC2 Using User Data Script

Use the following User Data while launching instances:

```bash
#!/bin/bash
apt update -y
apt install nginx -y

PRIVATE_IP=$(hostname -I | awk '{print $1}')

cat <<EOF > /var/www/html/index.html
<!DOCTYPE html>
<html>
<head>
<title>Load Balancer Test</title>
</head>
<body>
<h1>Application Load Balancer Test</h1>
<p>Served from EC2 Instance</p>
<p><strong>Private IP:</strong> $PRIVATE_IP</p>
</body>
</html>
EOF

systemctl start nginx
systemctl enable nginx
This script:

Installs Nginx

Creates sample webpage

Displays instance IP

Step 3: Create Target Group

EC2 → Target Groups → Create

Target type: Instances

Protocol: HTTP

Port: 80

Register all three EC2 instances

Configure health checks

Step 4: Create Security Groups
ALB Security Group

Allow HTTP (80) from Anywhere

EC2 Security Group

Allow HTTP (80) only from ALB Security Group

Allow SSH (22) from your IP

This protects backend servers from public access.

Step 5: Create Application Load Balancer

EC2 → Load Balancers → Create ALB

Internet-facing

Select public subnets (Multi-AZ)

Attach ALB Security Group

Associate Target Group

Step 6: Configure Listener Rules

Listener: HTTP :80

Forward traffic to target group

Step 7: Test Load Balancing

Copy ALB DNS Name

Open in browser

Refresh page multiple times

Observe Private IP changes

This confirms traffic distribution.

Step 8: Validate High Availability

Stop one EC2 instance

Refresh ALB URL

Website still works via remaining instances

🔄 End-to-End Traffic Flow
User → ALB → Target Group → EC2 Instance → Nginx → Response

📈 Outcomes

Traffic evenly distributed

High availability achieved

Backend instances protected

Production-style architecture implemented

🔐 Security Highlights

EC2 not directly exposed

ALB acts as single entry point

Security groups restrict access

Health checks ensure reliability