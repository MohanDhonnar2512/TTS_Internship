# 📸 AWS EC2 Snapshot & EBS Volume Management Project

## 📌 Project Overview

This project demonstrates how to manage **Amazon EC2 EBS volumes and snapshots**.  
It covers creating EC2 instances, attaching additional EBS volumes, taking manual snapshots, restoring volumes from snapshots, copying snapshots across regions, and verifying recovered data.

This project is useful for learning **AWS backup, disaster recovery, and storage management concepts**.

---

## 🛠️ Technologies & Services Used

- **Amazon Web Services (AWS)**
  - EC2 (Elastic Compute Cloud)
  - EBS (Elastic Block Store)
  - Snapshots
  - AMI
- **Operating System**
  - Ubuntu 22.04
- **Tools**
  - AWS Management Console
  - SSH (PuTTY / Terminal)

---

## 🏗️ Architecture


---

## 🎯 Project Objectives

- Launch EC2 instance
- Attach additional EBS volume
- Format and mount volume
- Add sample data
- Create manual snapshot
- Restore volume from snapshot
- Attach restored volume to new EC2
- Copy snapshot to another AWS region
- Verify recovered data

---

## ✅ Prerequisites

- AWS Account
- Basic Linux commands knowledge
- SSH client (PuTTY / Terminal)
- EC2 Key Pair

---

## 🔄 Step-by-Step Implementation

---

### Step 1: Launch EC2 Instance

- Go to **EC2 → Instances → Launch Instance**
- Select **Ubuntu 22.04**
- Instance type: `t2.micro`
- Configure key pair
- Security Group:
  - SSH (22)
  - Allow all traffic (for lab purpose)
- Launch instance

---

### Step 2: Attach Additional EBS Volume

1. EC2 → Volumes → Create Volume  
2. Size: **10 GB**  
3. Availability Zone: Same as EC2  
4. Create Volume  
5. Select volume → Actions → Attach Volume  
6. Select EC2 instance  
7. Device: `/dev/sdf`

---

### Step 3: Format and Mount Volume

SSH into EC2:

```bash
lsblk
sudo mkfs.ext4 /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data
 

 Step 4: Add Sample Data
cd /data
sudo touch sample.txt
echo "Snapshot Test Data" | sudo tee sample.txt

Step 5: Take Manual Snapshot

EC2 → Volumes

Select attached volume

Actions → Create Snapshot

Name: data-volume-snapshot

Wait until status becomes Completed

Step 6: Create Volume from Snapshot

EC2 → Snapshots

Select snapshot

Actions → Create Volume

Choose same Availability Zone

Step 7: Attach Restored Volume to New Instance

Launch second EC2 instance

Attach restored volume to it

Step 8: Mount and Verify Data

SSH into second EC2:

sudo mkdir /restore
sudo mount /dev/xvdf /restore
cat /restore/sample.txt

Step 9: Copy Snapshot to Another Region

EC2 → Snapshots

Select snapshot → Copy Snapshot

Destination Region: Singapore

Copy

Verify by switching region.

Step 10: Create Volume from Copied Snapshot

Switch to destination region

EC2 → Snapshots

Select snapshot → Create Volume

Attach to EC2 if required

📂 Project Flow Summary
EC2 → EBS Volume → Snapshot → Restore Volume → New EC2
                     |
                     v
            Cross Region Copy

🔐 Key Concepts Learned

EBS Volume attachment

Manual Snapshots

Volume restoration

Cross-region snapshot copy

Disaster recovery basics

Data verification