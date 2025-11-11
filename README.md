# 🌐 Terraform Secure WebApp on AWS

## 📘 Overview
This project uses **Terraform** to build a **secure, scalable web application architecture** on **AWS**.  
It provisions a full environment with **VPC, public/private subnets, EC2 instances, Security Groups, and an Application Load Balancer (ALB)**.

The goal is to automate infrastructure deployment and demonstrate best practices for isolating public and private resources while ensuring secure network communication.

<img width="1366" height="725" alt="image" src="https://github.com/user-attachments/assets/8f8779e6-26db-49eb-86ef-a617c7a87a18" />

---

## 🧱 Architecture
The infrastructure includes:

- **VPC** with public and private subnets in two availability zones.
- **Internet Gateway** and **NAT Gateway** for secure outbound access.
- **Security Groups** separating public (nginx) and private (backend) tiers.
- **EC2 Instances**
  - *Public Tier*: Nginx reverse proxies.
  - *Private Tier*: Python backend service.
- **Application Load Balancer (ALB)** routing HTTP traffic to public EC2.
- **Terraform Outputs** showing VPC info and ALB DNS endpoint.

---

## 🧩 Modules
| Module | Purpose |
|--------|----------|
| `vpc`  | Creates the VPC, subnets, Internet Gateway, and NAT Gateway |
| `ec2`  | Deploys EC2 instances (public and private) with proper security groups |
| `alb`  | Creates an Application Load Balancer and target groups |

<img width="1647" height="632" alt="image" src="https://github.com/user-attachments/assets/67347406-51d6-4cb6-87ed-8c87124ad9e6" />

<img width="1643" height="288" alt="image" src="https://github.com/user-attachments/assets/04e30d8b-8f2b-4c49-9f41-e84284ba2147" />

<img width="1616" height="777" alt="image" src="https://github.com/user-attachments/assets/da82c767-3e90-499b-9627-2e197ae1786c" />

---

## 🚀 How to Deploy
```bash
git clone https://github.com/mohamed-elatar/terraform-secure-webapp.git
cd terraform-secure-webapp
terraform init
terraform plan
terraform apply -auto-approve
```
<img width="1200" height="583" alt="image" src="https://github.com/user-attachments/assets/f5272acc-9370-4394-ba42-275c8cca0de8" />


```bash
#####################################################################################

To view the app:
terraform output public_alb_dns
```
<img width="760" height="91" alt="image" src="https://github.com/user-attachments/assets/d3f1f3e4-41fa-4471-8363-c3477b60cf75" />


```bash
🔒 Security Notes
.terraform/ ignored by .gitignore
Public access limited to HTTP(80) and SSH(22)
Private EC2s reachable only from public tier
Sensitive outputs hidden
```

```bash
########################################################################################


🧹 Cleanup
terraform destroy -auto-approve
```
<img width="1018" height="594" alt="image" src="https://github.com/user-attachments/assets/0de1e1a1-2efe-41cd-ad0c-360d506400d6" />
