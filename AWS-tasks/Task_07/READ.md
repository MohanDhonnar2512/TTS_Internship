
# 📦 AWS AMI Sharing Between Accounts

## 📌 Project Overview

This project demonstrates how to **create and share an Amazon Machine Image (AMI)** from one AWS account to another.

AMI sharing allows you to:

- Reuse pre-configured environments
- Standardize deployments
- Enable cross-account collaboration

This is commonly used in **enterprise environments** for distributing base images.

---

## 🎯 Project Objectives

- Create a custom AMI from EC2
- Share AMI with another AWS account
- Launch EC2 using shared AMI
- Understand permissions and security

---

## 🛠️ AWS Services Used

- Amazon EC2  
- AMI (Amazon Machine Image)  
- EBS Snapshots  
- IAM  
- Security Groups  

---

## 🏗️ Architecture
Source AWS Account -> Create AMI -> AMI + Snapshot -> Share Permissions -> Target AWS Account -> Launch EC2 -> New EC2 Instance (Same Configuration)

<img width="721" height="441" alt="image" src="https://github.com/user-attachments/assets/37c5b74b-aff4-4cae-86df-dbb19e533515" />



---

## ✅ Prerequisites

- Two AWS Accounts  
- EC2 Instance running in source account  
- Basic AWS knowledge  

---

## Step-by-Step Implementation

---

### Step 1: Launch and Configure EC2 (Source Account)

- Launch EC2 instance
- Install required software (e.g., Nginx)

```bash
sudo apt update
sudo apt install nginx -y
```
### Step 2: Create AMI

- Go to EC2 Dashboard
- Select instance
- Click Actions → Image → Create Image
- Provide name and description

📌 This creates:
AMI
Associated EBS Snapshot

### Step 3: Share AMI
- Go to AMIs → Select AMI
- Click Permissions → Edit
- Add Target AWS Account ID

### Step 4: Share Snapshot (Important)
- Go to Snapshots
- Select snapshot linked to AMI
- Click Permissions → Edit
- Add target account ID

⚠️ Without snapshot sharing, AMI will NOT work.

###  Step 5: Access AMI in Target Account
- Login to target AWS account
- Go to EC2 → AMIs → Private AMIs
-Locate shared AMI

### Step 6: Launch EC2 from Shared AMI
- Select shared AMI
- Launch instance
- Configure security group and key pair

### Step 7: Validate Deployment
- Connect to new EC2
- Verify installed software
- nginx -v
- Access via browser

##  Security Considerations
- Share AMI only with trusted accounts
- Use IAM policies to restrict access
- Avoid embedding sensitive data in AMI

##  Outcomes
- Cross-account resource sharing achieved
- Standardized environment deployment
- Faster infrastructure provisioning

## Common Mistakes
- ❌ Not sharing snapshot
- ❌ Wrong account ID
- ❌ Region mismatch
- ❌ Missing permissions

## Conclusion

This project demonstrates AMI creation and sharing, a key AWS skill used in real-world DevOps and cloud environments for scalable and consistent deployments.

