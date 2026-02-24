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

1.  **Build & Push**: 
    - The GitHub Action runner builds the Docker images for Frontend and Backend.
    - Images are tagged and pushed to Docker Hub (`vansh23100/dollar-frontend`, `vansh23100/dollar-backend`).
    
    > **Note on Architecture:** We build images on GitHub runners instead of the EC2 instance. The AWS `t3.micro` instance (1 vCPU, 1GB RAM) experiences CPU spikes of >80% during the build process (especially `npm install` and Angular builds), causing the instance to hang. Offloading the build process to GitHub Actions ensures stability and speed.

2.  **Deploy**:
    - The runner SSHs into the EC2 instance using `appleboy/ssh-action`.
    - It executes `docker-compose pull` to fetch the new images.
    - It restarts the containers using `docker-compose up -d`.

## 📝 Step-by-Step Setup & Deployment

### 1. Prerequisites
- **AWS EC2 Instance**: Ubuntu 22.04 (t3.micro).
- **Security Group**: Open ports `80` (HTTP), `22` (SSH)
- **Docker Installed**:
  ```bash
  sudo apt-get update
  sudo apt-get install -y docker.io docker-compose-plugin
  sudo usermod -aG docker ubuntu
  ```

### 2. Manual Deployment
Clone the repo and start services:
```bash
git clone <repo_url>
cd dollar_assignment
docker-compose up -d
```
