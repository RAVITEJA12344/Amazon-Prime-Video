📺 Amazon Prime Clone – DevOps CI/CD Pipeline on AWS EKS

This project demonstrates a complete end-to-end DevOps pipeline for deploying an Amazon Prime Clone application using modern DevOps tools like Terraform, Jenkins, SonarQube, Trivy, Docker, ECR, Kubernetes, EKS, ArgoCD, Prometheus, and Grafana.

The pipeline fully automates infrastructure provisioning, CI/CD, security scanning, containerization, GitOps-based deployment, and monitoring.

🚀 Architecture Overview
GitHub → Jenkins → SonarQube → Trivy → Docker → ECR → ArgoCD → EKS → Prometheus/Grafana

🧰 Tools & Technologies Used
Category	Tools
IaC	Terraform
Version Control	GitHub
CI/CD	Jenkins
Code Quality	SonarQube
Build Tool	NPM
Security Scan	Aqua Trivy
Containerization	Docker
Image Registry	AWS ECR
Orchestration	Kubernetes (AWS EKS)
GitOps Deployment	ArgoCD
Monitoring	Prometheus & Grafana
Cloud Provider	AWS
📦 Project Features

Fully automated AWS infrastructure creation using Terraform

Complete CI/CD pipeline using Jenkins

Static code analysis through SonarQube Quality Gates

Docker image build + vulnerability scan using Trivy

Image push to ECR

Deployment to EKS using ArgoCD GitOps

Real-time monitoring using Prometheus & Grafana

Zero-downtime deployments

⚙️ Prerequisites

AWS Account

AWS CLI installed & configured

Terraform installed

Git installed

VS Code (optional)

ArgoCD installed (optional if not using UI)

🏗️ 1. Infrastructure Setup Using Terraform
Clone the Repository
git clone https://github.com/your-repo/amazon-prime-clone-devops.git
cd amazon-prime-clone-devops

Terraform Commands
terraform init
terraform plan
terraform apply --auto-approve


Terraform provisions:

EC2 instance (Jenkins + SonarQube + Docker)

EKS Cluster

ECR Repository

Security Groups & IAM roles

🔐 2. SonarQube Setup

URL: http://<EC2-IP>:9000

Default login:

username: admin
password: admin


Generate a token:
Administration → Security → Users → Tokens

Save the token for Jenkins integration

🔧 3. Jenkins Configuration
Install Plugins

SonarQube Scanner

Docker

NodeJS

AWS Credentials

Prometheus Metrics

Kubernetes CLI

Add Credentials

SonarQube Token

AWS Access & Secret Key

Docker/ECR login

GitHub Token (optional)

Add Global Tools

JDK 17

NodeJS

SonarQube Scanner

Docker

📄 4. CI Pipeline Stages (Jenkins)

Checkout Code from GitHub

Run SonarQube Code Quality Analysis

NPM Install & Build

Trivy Vulnerability Scan

Docker Build

Tag & Push Image to ECR

Update Kubernetes manifest with new image tag

Commit to Git (ArgoCD triggers deployment)

☸️ 5. Deployment using ArgoCD (GitOps)
ArgoCD connects to the Kubernetes manifests repo

Deploys the Amazon Prime clone to EKS

Performs automatic syncing & rollouts

Provides real-time deployment status

ArgoCD UI Access
http://<ARGOCD-URL>

📊 6. Monitoring

Installed using Helm charts:

Prometheus: Collects metrics

Grafana: Visualizes cluster & app metrics

Dashboards include:

Node performance

Pod health

CPU & Memory usage

Deployment history

🧪 7. Project Pipeline Flow
Developer Commit → GitHub
      ↓
Jenkins CI Pipeline
      ↓
SonarQube Code Analysis
      ↓
Trivy Security Scan
      ↓
Docker Image Build
      ↓
Push to ECR
      ↓
Update Kubernetes YAML
      ↓
ArgoCD Sync
      ↓
Deployment to EKS
      ↓
Prometheus/Grafana Monitoring

🖥️ 8. Folder Structure
amazon-prime-clone/
│
├── terraform/
│   ├── ec2/
│   ├── eks/
│   └── variables.tf
│
├── jenkins/
│   └── Jenkinsfile
│
├── k8s-manifests/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
│
├── src/
│   ├── frontend/
│   └── backend/
└── README.md

🏁 Conclusion

This project demonstrates a complete DevOps CI/CD + GitOps workflow covering:

✔ IaC
✔ CI/CD
✔ Security
✔ Kubernetes Deployment
✔ Monitoring
✔ Cloud Automation

This makes the setup production-grade and fully automated with minimal manual effort.

If you want, I can also prepare:
