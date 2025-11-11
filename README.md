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


##################################################################################################################################

...existing code...
# Terraform Secure WebApp on AWS

## Overview
This repository contains Terraform code to provision a simple, secure web application architecture on AWS. It creates a VPC with public/private subnets, NAT/IGW, EC2 instances (public nginx proxies and private Python backends), and an Application Load Balancer (ALB).

Key files:
- Root configuration: [main.tf](main.tf) — modules are wired up via [`module.vpc`](main.tf), [`module.ec2`](main.tf) and [`module.alb`](main.tf)
- Provider: [providers.tf](providers.tf) — defines the [`provider "aws"`](providers.tf)
- Output: [outputs.tf](outputs.tf) — exposes [`module.alb.public_alb_dns`](outputs.tf)
- Modules:
  - VPC: [modules/vpc/main.tf](modules/vpc/main.tf) (creates [`aws_vpc.main`](modules/vpc/main.tf)), outputs in [modules/vpc/outputs.tf](modules/vpc/outputs.tf)
  - EC2: [modules/ec2/main.tf](modules/ec2/main.tf) (instances: [`aws_instance.public_proxy`](modules/ec2/main.tf), [`aws_instance.private_backend`](modules/ec2/main.tf); SGs: [`aws_security_group.public_sg`](modules/ec2/main.tf), [`aws_security_group.private_sg`](modules/ec2/main.tf)), outputs in [modules/ec2/outputs.tf](modules/ec2/outputs.tf)
  - ALB: [modules/alb/main.tf](modules/alb/main.tf) (load balancer: [`aws_lb.public_alb`](modules/alb/main.tf), target group: [`aws_lb_target_group.public_tg`](modules/alb/main.tf)), outputs in [modules/alb/outputs.tf](modules/alb/outputs.tf)

## Prerequisites
- Terraform v1.x
- AWS credentials configured (env or shared config)
- Recommended: run in a disposable/test AWS account

## Quickstart (deploy)
1. Initialize:
   ```sh
   terraform init
