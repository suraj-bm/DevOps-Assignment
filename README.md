<h1 align="center">🚀 DevOps Full-Stack Deployment on AWS</h1>

<h3 align="center">
Containerized Web Application | Terraform | Docker | CI/CD | AWS
</h3>

---

<h2 align="left">📌 Project Overview</h2>

This project demonstrates deployment of a full-stack containerized application on AWS using Infrastructure as Code and CI/CD automation.

<b>Frontend:</b> Next.js <br>
<b>Backend:</b> FastAPI <br>
<b>Reverse Proxy:</b> Nginx <br>
<b>Infrastructure:</b> Terraform <br>
<b>CI/CD:</b> GitHub Actions <br>
<b>Cloud Provider:</b> AWS (ap-south-1)

---

<h2 align="left">🏗 Architecture</h2>

<pre>
User Browser
      ↓
Internet
      ↓
EC2 Public IP
      ↓
Nginx (Reverse Proxy)
      ↓
 ┌───────────────┬───────────────┐
 │               │               │
Frontend       Backend          ....
(Next.js)      (FastAPI)
</pre>

---

<h2 align="left">☁️ Cloud & Region Choice</h2>

<b>AWS</b> was selected due to:

- Strong Terraform integration
- Mature networking model
- Industry adoption
- Cost-effective free tier

<b>Region:</b> ap-south-1 (Mumbai)

- Low latency for India
- Free-tier eligible instance types
- Cost efficiency

---

<h2 align="left">🧱 Infrastructure Decisions</h2>

<b>Custom VPC</b>
- Defined CIDR: 10.0.0.0/16
- Public Subnet: 10.0.1.0/24
- Internet Gateway
- Route Table (0.0.0.0/0 → IGW)

<b>Security Group</b>
- HTTP (80)
- SSH (22 - key-based authentication)

<b>EC2 Instance</b>
- Runs Docker & Docker Compose
- Hosts all application containers

<b>Why EC2 over Kubernetes?</b>
- Lower complexity
- Faster deployment
- Cost-efficient
- Suitable for small-scale workloads

---

<h2 align="left">🚀 Deployment Flow</h2>

<b>Infrastructure Provisioning:</b>

<pre>
terraform init
terraform plan
terraform apply
</pre>

<b>Application Deployment:</b>

<pre>
Docker installed
Repository cloned
Containers built
Application exposed on port 80
</pre>

---

<h2 align="left">🔁 CI/CD Pipeline</h2>

GitHub Actions automates deployment.

<pre>
Push to main branch
        ↓
GitHub Actions triggered
        ↓
SSH into EC2
        ↓
Pull latest code
        ↓
Rebuild Docker images
        ↓
Restart containers
</pre>

Benefits:
- Eliminates manual deployment
- Ensures consistency
- Reduces downtime

---

<h2 align="left">📈 Scaling & Failure Handling</h2>

<b>Current Setup:</b>
- Single EC2 instance
- Docker restart policy enabled
- No load balancer

<b>Failure Handling:</b>
- Container crash → Auto-restart
- EC2 failure → Downtime

<b>Future Scaling:</b>
- Add Application Load Balancer
- Auto Scaling Group
- Move backend to private subnet
- Use ECS or Kubernetes
- Host frontend on S3 + CloudFront

---

<h2 align="left">⚖ Tradeoffs & Limitations</h2>

- Single point of failure
- No HTTPS (ACM not configured)
- No monitoring stack
- No blue-green deployment
- No centralized logging

Tradeoff: Prioritized simplicity and cost efficiency over high availability.

---

<h2 align="left">🚀 Future Improvements</h2>

- HTTPS with ACM
- Load Balancer integration
- Auto Scaling
- Monitoring with CloudWatch
- Docker image registry (ECR)
- Multi-region deployment

---

<h2 align="center">🎯 Project Outcome</h2>

✔ Infrastructure as Code  
✔ Custom AWS networking  
✔ Containerized architecture  
✔ Reverse proxy configuration  
✔ Automated CI/CD pipeline  
✔ Scalable future-ready design  

---
