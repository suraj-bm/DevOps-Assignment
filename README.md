🚀 DevOps Deployment Documentation
📌 Project Overview

This project demonstrates the deployment of a full-stack containerized web application on AWS using Infrastructure as Code and CI/CD automation.

The solution includes:

Frontend: Next.js

Backend: FastAPI

Reverse Proxy: Nginx

Containerization: Docker & Docker Compose

Infrastructure Provisioning: Terraform

CI/CD Pipeline: GitHub Actions

Cloud Provider: AWS (ap-south-1)

The goal was to design a secure, reproducible, and automated deployment architecture while maintaining simplicity and cost efficiency.

🏗 Architecture Overview
High-Level Architecture

User Browser
→ Internet
→ EC2 Public IP
→ Nginx (Reverse Proxy)
→ Frontend Container
→ Backend Container

AWS Infrastructure Components

Custom VPC (10.0.0.0/16)

Public Subnet (10.0.1.0/24)

Internet Gateway

Route Table (0.0.0.0/0 → IGW)

Security Group

EC2 Instance (Docker Host)

Container Layer

Inside EC2:

Nginx listens on port 80

Routes / to frontend (port 3000)

Routes /api to backend (port 8000)

Containers communicate via Docker bridge network

🌍 Cloud & Region Choice
Cloud Provider: AWS

Reasons for selecting AWS:

Strong Terraform integration

Mature networking capabilities

Industry-standard IAM model

Widely adopted cloud platform

Region: ap-south-1 (Mumbai)

Reasons:

Lower latency for Indian users

Cost efficiency

Free-tier eligible instance types available

🧱 Infrastructure Design Decisions
1️⃣ Custom VPC

Instead of using the default VPC, a custom VPC was created to:

Demonstrate networking knowledge

Control CIDR blocks

Explicitly configure routing

2️⃣ Public Subnet

A public subnet was configured with:

Auto-assigned public IP

Route to Internet Gateway

This allows:

Application access from the internet

Outbound package downloads

3️⃣ Security Group

Inbound rules:

HTTP (80) – Public access

SSH (22) – Key-based authentication

Outbound:

Allow all traffic

4️⃣ EC2 Instead of Kubernetes

Chosen for:

Simplicity

Lower operational overhead

Cost efficiency

Suitable for small-scale workloads

5️⃣ Docker-Based Deployment

Docker ensures:

Environment consistency

Dependency isolation

Easy reproducibility

6️⃣ Nginx Reverse Proxy

Used to:

Route traffic cleanly

Separate frontend and backend

Enable future scaling flexibility

🚀 Deployment Workflow
Infrastructure Provisioning

Terraform Commands:

terraform init

terraform plan

terraform apply

Terraform provisions:

VPC

Subnet

Route table

Internet Gateway

Security Group

EC2 Instance

EC2 Bootstrap (User Data)

On launch:

Docker installed

Docker Compose installed

Git repository cloned

Containers built and started

🔁 CI/CD Pipeline

CI/CD implemented using GitHub Actions.

Flow:

Push to main branch
→ GitHub Actions triggered
→ SSH into EC2
→ Pull latest code
→ Rebuild Docker images
→ Restart containers

Benefits:

Eliminates manual deployment

Ensures consistent releases

Reduces human error

📈 Scaling Strategy
Current Setup

Single EC2 instance

Docker restart policy for container crashes

No auto scaling

If Traffic Increases

Possible improvements:

Add Application Load Balancer

Use Auto Scaling Group

Separate backend into private subnet

Use ECS or Kubernetes

Host frontend on S3 + CloudFront

⚠ Failure Handling
Current Failure Domain

If container crashes → Docker restarts it

If EC2 fails → Application downtime

Improvements for High Availability

Multi-AZ deployment

Auto Scaling

Load balancing

Health checks

⚖ Tradeoffs & Limitations
Limitations

Single point of failure (EC2)

No load balancer

No HTTPS/ACM

No centralized logging

No monitoring stack

No blue-green deployment

Tradeoffs

Chose:

Simplicity

Cost efficiency

Faster deployment

Over:

High availability

Complex orchestration

🚀 Future Enhancements

Implement HTTPS with ACM

Introduce Load Balancer

Move backend to private subnet

Use RDS for database

Implement monitoring (CloudWatch)

Add container registry (ECR)

Implement Blue-Green deployment strategy

Multi-region failover

🎯 Conclusion

This project demonstrates:

Infrastructure as Code using Terraform

Custom AWS networking configuration

Containerized full-stack deployment

Reverse proxy architecture

Automated CI/CD pipeline

Thoughtful infrastructure tradeoffs

The system is simple, reproducible, and production-structured, with clear pathways for scaling and resilience improvements.
