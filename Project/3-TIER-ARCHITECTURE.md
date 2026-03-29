
# AWS Three-Tier Architecture Deployment 

## 📌 Project Overview

This project implements a **Three-Tier Architecture on AWS**, separating an application into:

1. **Web Tier (Presentation Layer)**
2. **Application Tier (Business Logic Layer)**
3. **Database Tier (Data Layer)**

The architecture is deployed inside a **custom VPC** with **public and private subnets**, integrated with:

- Auto Scaling Groups
- Application Load Balancer
- NAT Gateway
- Amazon RDS (MySQL)

This design follows AWS best practices for:

✅ Security  
✅ Scalability  
✅ High Availability  
✅ Fault Tolerance  

---

## 🎯 Project Objectives

- Design secure three-tier architecture
- Deploy tiers in isolated subnets
- Implement Auto Scaling
- Use managed database (Amazon RDS)
- Enable outbound access using NAT Gateway
- Achieve production-grade availability

---

## 🛠️ AWS Services Used

- Amazon VPC  
- EC2  
- Auto Scaling Group  
- Application Load Balancer  
- Launch Templates  
- NAT Gateway  
- Internet Gateway  
- Amazon RDS (MySQL)  
- Security Groups  

---

## 🏗️ Architecture Diagram
![Architecture Diagram](https://github.com/user-attachments/assets/9a9297e7-97d2-41cf-a4f5-69008ac97a3c)


---

##  Network 

### VPC
CIDR: `10.0.0.0/16`

Provides isolated networking for all tiers.

---

### Subnets

#### Public Subnets (Web Tier)
- Two AZs
- Hosts Web EC2
- Connected to Internet Gateway

#### Private Subnets – Application Tier
- Two AZs
- Hosts Flask backend EC2
- Outbound access via NAT Gateway

#### Private Subnets – Database Tier
- Two AZs
- Hosts Amazon RDS
- Fully isolated from internet

---

##  Route Tables

### Public Route Table
0.0.0.0/0 → Internet Gateway

### Private Route Table
0.0.0.0/0 → NAT Gateway

---

##  Internet Gateway

- Enables public internet access for Web Tier
- Attached to VPC

---

##  NAT Gateway

Allows private EC2 instances to:

- Install packages
- Download updates
- Access external APIs

WITHOUT public exposure.

---

##  Security Groups

### Load Balancer SG
- HTTP 80 → Anywhere

### Web Tier SG
- HTTP 80 → ALB only
- SSH → Admin IP

### Application Tier SG
- HTTP 5000 → Web Tier only

### Database Tier SG
- MySQL 3306 → Application Tier only

---

## Launch Templates

Used for both Web and Application tiers.

Includes:

- Ubuntu AMI
- Instance Type (t2.micro / t3.micro)
- Security Group
- Key Pair
- User Data

Ensures consistent instance creation.

---

## Auto Scaling Groups

### Web Tier ASG
- Nginx servers
- Public subnets
- Connected to ALB

### Application Tier ASG
- Flask servers
- Private subnets

Benefits:
- Automatic scaling
- Fault tolerance
- Multi-AZ deployment

---

##  Web Tier Deployment (Nginx)

### Install Nginx
```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx

cd /var/www/html
sudo nano index.html
sudo nano style.css
sudo systemctl restart nginx
```

## ⚙️ Application Tier Deployment (Python + Flask)
Install Dependencies
```bash
sudo apt install python3 python3-pip -y
pip3 install flask

Run Application
python3 app.py


Flask handles:

Business logic

Database queries

Response formatting
```

## Database Tier – Amazon RDS (MySQL)
### Configuration


- Engine: MySQL

- Private Subnets

- Public Access: Disabled

- Multi-AZ Enabled

### Benefits:

- Automatic backups

- Failover

- Encryption

- No OS management

🔗 MySQL Client Connectivity

Installed on Application Tier:
```bash

sudo apt install mysql-client -y
mysql -h <RDS-ENDPOINT> -u admin -p
```

Used for:

- Query execution

- Connectivity validation

## Validation
Web Tier
```bash
curl http://localhost
```
Application Tier
```bash
curl http://localhost:5000
```
Database Tier
```bash
SHOW DATABASES;
```

## End-to-End Request Flow

1) User sends HTTP request

2) ALB receives traffic

3) Web Tier serves frontend

4) Flask processes backend logic

5) RDS executes query

6) Response returns to user

## Project Outcome

✅ Fully deployed Three-Tier Architecture
✅ Secure VPC networking
✅ Auto Scaling enabled
✅ NAT Gateway implemented
✅ Database isolated
✅ End-to-end flow validated
✅ Production-ready infrastructure
