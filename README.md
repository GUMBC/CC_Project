# AWS Scalable Cloud Architecture — Full Deployment (Terraform + CloudFormation)
_By Gayatri Thakur

This project implements a **highly available, scalable, three-tier architecture on AWS**, combining **Terraform**, **CloudFormation**, **EC2**, **RDS**, **ALB**, **S3**, and **Lambda**.  
The goal is to automate provisioning, enforce security, and validate full end-to-end connectivity across all services.

---

##
Project Architecture Overview
This setup follows AWS best practices for a secure 3-tier architecture:

### **1️⃣ Presentation Layer**
- Application Load Balancer (ALB)
- Public subnets (us-east-1a / us-east-1b)

### **2️⃣ Application Layer**
- EC2 Apache Web Server  
- Displays:  
  **“Hello from Gayatri’s EC2 — EC2 + ALB + RDS + S3 + Lambda are working.”**

### **3️⃣ Database Layer**
- RDS MySQL in private subnets  
- Accessible ONLY from EC2 SG

### **4️⃣ Storage & Serverless**
- S3 bucket  
- Lambda function  
- CloudWatch logs  

### **5️⃣ Networking**
- Custom VPC  
- 2 Public + 2 Private subnets  
- IGW + NAT Gateway  
- Route tables  

### **6️⃣ Security**
- ALB SG → allows HTTP (80) from internet  
- EC2 SG → allows HTTP ONLY from ALB  
- RDS SG → allows MySQL ONLY from EC2  
- No open ports to public internet on RDS  

---

##  Tools Used
- **Terraform** — VPC, Subnets, Routing, Security Groups  
- **CloudFormation** — EC2, ALB, Target Group, RDS, Lambda, S3  
- **AWS Services** — EC2, RDS, ALB, Lambda, S3, VPC, CloudWatch  

---

##  Deployment Workflow

### **PHASE 1 — Terraform (Infrastructure Foundation)**
Creates:
- VPC  
- Public + Private Subnets  
- Route Tables  
- Internet Gateway  
- NAT Gateway  
- Security Groups  
- Outputs for CloudFormation  

### **PHASE 2 — CloudFormation (Compute & Application Layer)**
Creates:
- EC2 Web Server (Apache installed automatically)  
- Application Load Balancer  
- Target Group + Listener  
- RDS MySQL Instance  
- S3 Bucket  
- Lambda Function + Execution Role  

---

## ✔ Validation Checklist

### **1. ALB Test**
Visit ALB DNS name  
- Apache page loads → confirms web + SG + ALB working  

### **2. RDS Test**
SSH into EC2 and run:

mysql -h <endpoint> -u adminuser -p
Confirms private networking and correct SG configuration.

### **3. S3 Test**
Upload + download files.

### **4. Lambda Test**
Run test from console → CloudWatch logs appear.

---

##  Challenges Faced
- Incorrect security group mappings  
- ALB “Unhealthy” due to Apache not installed / SG missing  
- RDS engine version mismatch  
- IAM permissions missing for Lambda → fixed  

---

## Final Outcomes
- Fully deployed **three-tier web architecture**  
- Secure networking (no public DB access)  
- Automated IaC workflow  
- Production-grade design suitable for scaling  

---

## Future Improvements
- Auto Scaling Group (ASG)  
- Multi-AZ RDS  
- Secrets Manager for database credentials  
- CI/CD with GitHub Actions  
- Docker + ECS / EKS migration  

---


---

## 👩‍💻 Author
**Gayatri Thakur
MSIS — University of Maryland, Baltimore County (UMBC)

