# 🌐 Terraform Secure WebApp on AWS

## 📘 Overview
This project uses **Terraform** to build a **secure, scalable web application architecture** on **AWS**.  
It provisions a full environment with **VPC, public/private subnets, EC2 instances, Security Groups, and an Application Load Balancer (ALB)**.

The goal is to automate infrastructure deployment and demonstrate best practices for isolating public and private resources while ensuring secure network communication.

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

---

## 🚀 How to Deploy
```bash
git clone https://github.com/mohamed-elatar/terraform-secure-webapp.git
cd terraform-secure-webapp
terraform init
terraform plan
terraform apply -auto-approve


#####################################################################################

To view the app:
terraform output public_alb_dns



🔒 Security Notes
.terraform/ ignored by .gitignore
Public access limited to HTTP(80) and SSH(22)
Private EC2s reachable only from public tier
Sensitive outputs hidden


########################################################################################


🧹 Cleanup
terraform destroy -auto-approve


#########################################################################################
