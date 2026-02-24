# MEAN Stack DevOps Assignment

## 🚀 Overview
Full-stack MEAN application containerized with Docker and deployed via CI/CD pipelines to an AWS EC2 instance using Nginx as a reverse proxy.

## 🛠️ Infrastructure & Tech Stack
- **Frontend**: Angular 15 (Nginx)
- **Backend**: Node.js & Express
- **Database**: MongoDB (Containerized)
- **CI/CD**: GitHub Actions
- **Cloud**: AWS EC2 (Ubuntu t3.micro)
- **Orchestration**: Docker Compose

## ⚙️ CI/CD Configuration

The pipeline (`.github/workflows/deploy.yml`) automates the build and deployment process:

1. **Build & Test**: Separate jobs for frontend and backend with NPM caching.
2. **Push to Registry**: Images built and pushed to Docker Hub only on main branch.
3. **Deploy to VM**: Automatic deployment via SSH after successful push.

> **Note on Architecture:** We build images on GitHub runners instead of the EC2 instance. The AWS `t3.micro` instance (1 vCPU, 1GB RAM) experiences CPU spikes of >80% during the build process, causing the instance to hang. Offloading the build process to GitHub Actions ensures stability and speed.

## 📝 Step-by-Step Setup & Deployment

### 1. Prerequisites
- **AWS EC2 Instance**: Ubuntu 22.04 (t3.micro).
- **Security Group**: Open ports `80` (HTTP), `22` (SSH).
- **Docker Installed**:
  ```bash
  sudo apt-get update
  sudo apt-get install -y docker.io docker-compose-plugin
  sudo usermod -aG docker ubuntu
  ```

### 2. Initial Server Setup
```bash
git clone <repo_url>
cd dollar_assignment
docker compose up -d
```

### 3. CI/CD Secrets Configuration
Add these secrets in **Settings > Secrets and variables > Actions**:
- `DOCKERHUB_USERNAME`: Docker Hub username
- `DOCKERHUB_TOKEN`: Docker Hub access token
- `SSH_HOST`: EC2 public IP
- `SSH_USER`: EC2 username
- `SSH_KEY`: Private SSH key content
- `SSH_PORT`: EC2 SSH port

## 📸 Screenshots & Proof of Work

### 1️⃣ CI/CD Configuration & Execution


### 2️⃣ Docker Image Build & Push Process

### 3️⃣ Application Deployment & Working UI

### 4️⃣ Nginx Setup & Infrastructure Details
