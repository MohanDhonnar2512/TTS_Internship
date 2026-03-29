
# Live Cloud Infrastructure Management on AWS 

## Project Overview

This project demonstrates the deployment and management of a
production-style cloud infrastructure using Amazon Web Services (AWS).
The infrastructure supports multi-server web hosting, secure networking,
monitoring, backup management, and DNS configuration.

The goal of the project is to simulate real-world cloud infrastructure
operations including server deployment, access control, monitoring, and
disaster recovery strategies.

------------------------------------------------------------------------

## Technologies Used

-   Amazon Web Services (AWS)
-   Amazon EC2
-   AWS Security Groups
-   Amazon CloudWatch
-   Amazon Route 53
-   Amazon Machine Image (AMI)
-   Amazon EBS Snapshots
-   AWS Identity and Access Management (IAM)
-   SSL / HTTPS

------------------------------------------------------------------------

## Infrastructure Architecture

User Request\
↓\
Route 53 DNS Resolution\
↓\
EC2 Web Servers\
↓\
Security Groups (Network Control)\
↓\
CloudWatch Monitoring\
↓\
Backup System (AMI & Snapshots)

------------------------------------------------------------------------

## EC2 Instance Deployment

Multiple EC2 instances were launched to host web applications.

### Instance Configuration

-   Instance Type: t2.micro / t3.micro
-   Operating System: Ubuntu/window
-   Key Pair: SSH/RDP authentication
-   Elastic IP for public access
-   Web server installed (Nginx)

### Basic Server Setup

``` bash
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

------------------------------------------------------------------------

## Network Security Configuration

Security groups control inbound and outbound traffic.

### Inbound Rules

  Port   Protocol   Purpose
  ------ ---------- ----------------------
-  22     SSH        Secure server access
-  80     HTTP       Web traffic
-  443    HTTPS      Secure web traffic
-  3389   RDP        Remote Desktop 

### Security Practices

-   Restrict SSH access to specific IP ranges
-   Allow only required ports
-   Apply least privilege rules

------------------------------------------------------------------------

## Identity and Access Management (IAM)

Access to AWS resources is controlled using IAM.

### IAM Components

**IAM Users** - Created for administrators and developers

**IAM Groups** - Admin Group -- full AWS access - DevOps Group --
infrastructure management - Developer Group -- limited deployment access

**IAM Roles** Used to allow AWS services to interact securely.

Examples: - EC2 instances sending logs to CloudWatch - Backup services
accessing EBS snapshots

**IAM Policies** Policies define permissions for AWS resources.

Examples: - EC2 management - CloudWatch monitoring - Route 53 DNS
management - Snapshot and AMI creation

### Security Best Practices

-   Enable Multi-Factor Authentication (MFA)
-   Limit root account usage
-   Implement role-based access control
-   Follow least privilege principle

------------------------------------------------------------------------

## Monitoring and Performance Management

Monitoring is implemented using Amazon CloudWatch.

### Metrics Monitored

-   CPU utilization
-   Network traffic
-   Disk operations
-   Instance health checks

### Alerts

CloudWatch alarms trigger alerts when: - CPU exceeds defined threshold -
Instances become unhealthy - Performance issues occur

------------------------------------------------------------------------

## Backup and Disaster Recovery

### Amazon Machine Images (AMI)

AMIs capture the complete configuration of an EC2 instance including OS,
applications, and settings. These images allow fast server recovery and
migration.

### EBS Snapshots

Snapshots provide incremental backups of storage volumes and enable
quick data recovery.

------------------------------------------------------------------------

## Domain and DNS Management

DNS routing is managed using Amazon Route 53.

Features include: - Domain mapping to EC2 public IP - Reliable DNS
resolution - High availability routing

------------------------------------------------------------------------

## SSL / HTTPS Configuration

SSL certificates enable secure encrypted communication between users and
the web server.

Benefits: - Secure data transmission - HTTPS access - Improved user
trust and security

------------------------------------------------------------------------

## Environment Support

### Production Environment

Live environment serving real user traffic.

### Testing Environment

Used to validate infrastructure changes before production deployment.

### Assessment / Development Environment

Used for experimentation and infrastructure testing.

------------------------------------------------------------------------

## Key Learning Outcomes

-   Deployment and management of EC2 servers
-   Secure networking using security groups
-   Monitoring infrastructure with CloudWatch
-   Backup and recovery using AMI and snapshots
-   DNS management using Route 53
-   Access control using IAM
-   Managing multiple cloud environments

------------------------------------------------------------------------

## Repository Purpose

This repository documents the architecture, configuration, and
operational practices involved in managing AWS cloud infrastructure.
