Project Overview
This project demonstrates deploying an Amazon Prime clone using a set of DevOps tools and practices. The primary tools include:

Terraform: Infrastructure as Code (IaC) tool to create AWS infrastructure such as EC2 instances and EKS clusters.
GitHub: Source code management.
Jenkins: CI/CD automation tool.
SonarQube: Code quality analysis and quality gate tool.
NPM: Build tool for NodeJS.
Aqua Trivy: Security vulnerability scanner.
Docker: Containerization tool to create images.
AWS ECR: Repository to store Docker images.
AWS EKS: Container management platform.
ArgoCD: Continuous deployment tool.
Prometheus & Grafana: Monitoring and alerting tools.
Pre-requisites
AWS Account: Ensure you have an AWS account. Create an AWS Account
AWS CLI: Install AWS CLI on your local machine. AWS CLI Installation Guide
VS Code (Optional): Download and install VS Code as a code editor. VS Code Download
Install Terraform in Windows: Download and install Terraform in Windows Terraform in Windows
Configuration
AWS Setup
IAM User: Create an IAM user and generate the access and secret keys to configure your machine with AWS.
Key Pair: Create a key pair named key for accessing your EC2 instances.
Infrastructure Setup Using Terraform
Clone the Repository (Open Command Prompt & run below):
git clone https://github.com/pandacloud1/DevopsProject2.git
cd DevopsProject2
code .   # this command will open VS code in backend
Initialize and Apply Terraform:
Run the below commands to reduce the path displayed in VS Code terminal (Optional)
code $PROFILE
function prompt {"$PWD > "}
function prompt {$(Get-Location -Leaf) + " > "}
Open terraform_code/ec2_server/main.tf in VS Code.
Run the following commands:
aws configure
terraform init
terraform apply --auto-approve
This will create the EC2 instance, security groups, and install necessary tools like Jenkins, Docker, SonarQube, etc.

SonarQube Configuration
Login Credentials: Use admin for both username and password.
Generate SonarQube Token:
Create a token under Administration → Security → Users → Tokens.
Save the token for integration with Jenkins.
Jenkins Configuration
Add Jenkins Credentials:

Add the SonarQube token, AWS access key, and secret key in Manage Jenkins → Credentials → System → Global credentials.
Install Required Plugins:

Install plugins such as SonarQube Scanner, NodeJS, Docker, and Prometheus metrics under Manage Jenkins → Plugins.
Global Tool Configuration:

Set up tools like JDK 17, SonarQube Scanner, NodeJS, and Docker under Manage Jenkins → Global Tool Configuration.
