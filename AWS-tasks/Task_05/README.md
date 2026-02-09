# 🚀 AWS Auto Scaling Group with Application Load Balancer

## 📌 Project Overview

This project demonstrates how to build a **highly available, scalable, and fault-tolerant web infrastructure** on AWS using:

- Auto Scaling Groups (ASG)
- Application Load Balancer (ALB)
- Multiple EC2 instances running Nginx

The system automatically **adds or removes EC2 instances based on traffic demand** and replaces unhealthy instances without downtime.

This setup represents a **production-ready AWS architecture**.

---

## 🛠️ Technologies & Services Used

- **Amazon Web Services (AWS)**
  - EC2
  - Auto Scaling Group
  - Application Load Balancer
  - Target Groups
  - Launch Templates
  - Security Groups
- **Operating System**
  - Ubuntu Linux
- **Web Server**
  - Nginx

---

## 🏗️ Architecture


---

## 🎯 Objective

- Automatically manage EC2 instances based on traffic
- Distribute traffic using ALB
- Maintain high availability across Availability Zones
- Enable automatic recovery from failures
- Achieve zero-downtime scaling

---

## ✅ Prerequisites

- AWS Account
- Basic EC2 and networking knowledge
- Understanding of Load Balancers
- Web browser

---

## 🔄 Step-by-Step Implementation

---

### Step 1: Prepare Network Environment

- Use existing VPC
- Select multiple public subnets (Multi-AZ)
- Ensure Internet Gateway and route tables are configured

This allows ASG to launch instances across Availability Zones.

---

### Step 2: Create Security Groups

#### Load Balancer Security Group
- Allow inbound HTTP (80) from Anywhere

#### EC2 Instance Security Group
- Allow inbound HTTP (80) only from ALB security group
- Allow SSH (22) from your IP

Backend servers remain protected from public access.

---

### Step 3: Create Launch Template – Web Template 1

Configuration:
- Ubuntu AMI
- Free-tier instance type
- Key pair
- EC2 security group
- User Data script

User Data installs Nginx and deploys a sample webpage.

---

### Step 4: Create Launch Template – Web Template 2

Same configuration as Template 1 but with:

- Different HTML message / version identifier

This demonstrates instance variation within Auto Scaling.

---

### Step 5: Create Target Group

- Target type: Instances  
- Protocol: HTTP  
- Port: 80  
- Health checks enabled  
- No manual instance registration (ASG handles this)

---

### Step 6: Create Application Load Balancer (ALB)

- Internet-facing ALB
- Attach public subnets (Multi-AZ)
- Assign ALB security group
- Associate with target group

---

### Step 7: Create Auto Scaling Group (ASG)

- Use Mixed Instance Policy
- Attach Launch Template 1 & 2
- Select multiple Availability Zones

Capacity:
- Minimum: 1  
- Desired: 2  
- Maximum: 4  

---

### Step 8: Attach Load Balancer to ASG

- Attach Target Group to ASG
- ALB performs health checks
- Unhealthy instances replaced automatically

---

### Step 9: Configure Scaling Policies

- Target tracking scaling
- Metric: Average CPU Utilization
- Scale out when CPU increases
- Scale in when demand drops

Ensures cost-efficient elasticity.

---

### Step 10: Launch and Validate Auto Scaling

Testing:
- Access ALB DNS name
- Refresh page to observe different instances
- Generate CPU load to trigger scale-out
- Stop one instance to verify automatic replacement

---

## 🔄 End-to-End Traffic Flow

User → ALB → Target Group → Auto Scaling Group → EC2 → Nginx → Response

---

## 📈 Outcomes

- Load-balanced auto-scaling infrastructure
- High availability across Availability Zones
- Automatic recovery from failures
- Zero-downtime scaling
- Secure backend servers

---


