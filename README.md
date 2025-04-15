
```markdown
# Docker, Kubernetes, Terraform, AWS SDK, ECR, EKS, and CI/CD Setup

This repository contains multiple projects related to Docker, Kubernetes, Terraform, AWS SDK, ECR, EKS, and CI/CD pipelines. Each section below describes how to set up and run the respective project.

---

## 1️⃣ Dockerized Flask App

A simple Python Flask web app running inside a Docker container.

### 🚀 Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/my-python-app.git
   cd my-python-app
   ```

2. **Build the Docker Image:**
   ```bash
   docker build -t my-python-app .
   ```

3. **Run the Docker Container:**
   ```bash
   docker run -d -p 5000:5000 --name flask-container my-python-app
   ```

4. **Check the App in Docker Desktop:**
   - View logs
   - Access the container shell

5. **View the Web App in Browser:**
   Open `http://localhost:5000` to see "Hello from Docker!"

---

## 2️⃣ Minikube Kubernetes: Running Kubernetes Locally

Set up Kubernetes locally using Minikube.

### 🛠️ Prerequisites
- kubectl
- Minikube

### Step 1: Start Minikube
```bash
minikube start
```

### Step 2: Open Minikube Dashboard
```bash
minikube dashboard
```

### Step 3: Deploy a Simple App
```bash
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
```

---

## 3️⃣ Terraform AWS Infrastructure Setup

This project automates the creation of a VPC, Subnet, and EC2 Instance in AWS using Terraform.

### 🛠️ Prerequisites
- Terraform
- AWS CLI

### 🧑‍💻 Terraform Configuration
1. Initialize Terraform with `terraform init`.
2. Plan the infrastructure with `terraform plan`.
3. Apply the configuration using `terraform apply`.

### Resources Created
- VPC
- Subnet
- EC2 Instance

### Clean Up
Run `terraform destroy` to delete the created resources.

---

## 4️⃣ AWS S3 Bucket Creation with Boto3 in VS Code

This project demonstrates how to create an AWS S3 bucket using the AWS SDK for Python (Boto3) in **VS Code**.

### 🛠️ Tools Used
- Python 3.x
- Visual Studio Code (VS Code)
- AWS SDK for Python (Boto3)
- AWS CLI

### 📁 Project Files
- `code.py` — Python script to create an S3 bucket.
- `results.txt` — Contains sample output: `Hello from AWS SDK!`

### ✅ Steps to Run
1. Open VS Code and create a folder for your project.
2. Create a file `code.py` with the provided Python script to create the S3 bucket.
3. Set up AWS CLI with `aws configure` (configure your AWS Access Key, Secret Key, and Region).
4. Install Boto3 with `pip install boto3`.
5. Run the script using `python code.py`.

---

## 5️⃣ Capital Finder App – Deploying a Dockerized .NET App to AWS EKS

This guide helps you containerize your .NET application and deploy it to Amazon Elastic Kubernetes Service (EKS).

### 🛠️ Prerequisites
- AWS CLI
- Docker
- kubectl
- eksctl
- .NET SDK

### 🐳 Step 1: Dockerize the .NET App
Create a Dockerfile for the app:
```dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "CapitalFinderApp.dll"]
```

Build and run the Docker image:
```bash
docker build -t capital-finder-app .
```

### 📦 Step 2: Push Image to AWS ECR
1. Create a repository in ECR:  
   `aws ecr create-repository --repository-name capital-finder-app`
2. Authenticate Docker to ECR:
   ```bash
   aws ecr get-login-password --region us-east-1 | \
   docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com
   ```
3. Tag and push the image to ECR:
   ```bash
   docker tag capital-finder-app:latest 123456789012.dkr.ecr.us-east-1.amazonaws.com/capital-finder-app:latest
   docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/capital-finder-app:latest
   ```

### ☁️ Step 3: Create an EKS Cluster
```bash
eksctl create cluster \
--name capital-cluster \
--region us-east-1 \
--nodes 2 \
--node-type t3.medium \
--managed
```

### 🚀 Step 4: Deploy App to Kubernetes
Create a `deployment.yaml` file and apply it with `kubectl`.

### 🌐 Step 5: Access Your Application
Use the external IP from the LoadBalancer service to access your app in the browser.

---

## 6️⃣ Lambda CI/CD with GitHub Actions

This repository shows how to deploy an AWS Lambda function using CI/CD with GitHub Actions.

### 🛠️ Prerequisites
- Python 3.9+
- AWS CLI
- Git
- Visual Studio Code
- GitHub Account

### 🧑‍💻 Setup Instructions
1. Set up the Lambda function in a folder named `COUNTRYCAPITAL/lambda`.
2. Create the Lambda function and package it with the necessary dependencies.
3. Use AWS CLI to create the Lambda function.

### Part 6: Setup GitHub Actions
- Add the GitHub Actions workflow in `.github/workflows/lambda-deploy.yml`.

### Part 7: Add GitHub Secrets
Add `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` in GitHub secrets.

### Part 8: Verify Deployment
Verify the Lambda function through the AWS Lambda Console and test the function.

---

### 🧼 Clean Up
Use the following commands to clean up any created resources:
- **AWS Resources:** Follow the clean-up steps in each project.
- **Docker Containers:** `docker stop flask-container && docker rm flask-container`
- **Minikube:** `minikube delete`

---
