````markdown
# 🚀 RPS Game CI/CD Pipeline with Jenkins, Docker & Kubernetes (Kind)

## 📌 Project Overview

This project demonstrates an end-to-end CI/CD pipeline for deploying a Rock-Paper-Scissors (RPS) game application using modern DevOps practices. The entire deployment process is automated using **Jenkins**, where every code push to the GitHub repository triggers a pipeline that builds a Docker image, pushes it to a Docker Registry, and deploys the latest version to a Kubernetes cluster created using **Kind** on an AWS EC2 instance.

The application is exposed externally using a **NodePort Service**, allowing users to access the application through the EC2 public IP.

---

# 🎯 Objectives

- Automate application deployment using Jenkins CI/CD.
- Containerize the application using Docker.
- Store Docker images in Docker Registry.
- Deploy the application to Kubernetes.
- Expose the application using a NodePort Service.
- Automate the entire workflow from GitHub push to Kubernetes deployment.

---

# 🛠 Tech Stack

| Technology | Purpose |
|------------|---------|
| Git | Version Control |
| GitHub | Source Code Repository |
| Jenkins | CI/CD Automation |
| Docker | Containerization |
| Docker Registry | Store Docker Images |
| Kubernetes | Container Orchestration |
| Kind | Local Kubernetes Cluster |
| AWS EC2 | Infrastructure Hosting |
| NodePort Service | Expose Application |

---

# 🏗 Project Architecture

```text
                    Developer
                        │
                  Git Push to GitHub
                        │
                        ▼
                +----------------+
                |    Jenkins     |
                |  CI/CD Server  |
                +----------------+
                        │
        ---------------------------------
        │               │               │
        ▼               ▼               ▼
 Clone Repository   Build Docker    Execute Pipeline
                        Image
                          │
                          ▼
             Push Image to Docker Registry
                          │
                          ▼
             Kubernetes Cluster (Kind)
                          │
                Update Deployment
                          │
                          ▼
                  Kubernetes Pods
                          │
                          ▼
                 NodePort Service
                          │
                          ▼
                 Access Application
```

---

# 📂 Project Structure

```
RPS-Game/
│
├── Jenkinsfile
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── app/
│   ├── index.html
│   ├── style.css
│   └── script.js
├── screenshots/
└── README.md
```

---

# ⚙ Prerequisites

Before running this project, ensure the following tools are installed:

- Git
- Docker
- Jenkins
- kubectl
- Kind
- AWS EC2 Instance
- Docker Registry Account

---

# 🚀 Deployment Process

## Step 1: Launch an AWS EC2 Instance

An EC2 instance was created to host both Jenkins and the Kubernetes cluster.

Installed:

- Docker
- Jenkins
- kubectl
- Kind
- Git

---

## Step 2: Clone the Repository

```bash
git clone [https://github.com//RPS-Game.git](https://github.com/DhesiTheKing/RockPaperSissor.git)
```

---

## Step 3: Create Kubernetes Cluster using Kind

A Kubernetes cluster was created using Kind.

```bash
kind create cluster --name rps-cluster
```

Verify cluster:

```bash
kubectl cluster-info
```

Check nodes:

```bash
kubectl get nodes
```

---

## Step 4: Containerize the Application

A Dockerfile was created to package the application into a Docker image.

Build the image:

```bash
docker build -t jeevika37/rps-game:latest .
```

Run locally:

```bash
docker run -d -p 8080:80 jeevika37/rps-game:latest
```

---

## Step 5: Push Image to Docker Registry

Login:

```bash
docker login
```

Push image:

```bash
docker push jeevika37/rps-game:latest
```

The Docker Registry stores the latest application image, allowing Kubernetes to pull and deploy it.

---

## Step 6: Configure Kubernetes Deployment

Deployment YAML defines:

- Deployment
- Replica count
- Container image
- Container port

Deploy:

```bash
kubectl apply -f deployment.yaml
```

Verify:

```bash
kubectl get deployments
kubectl get pods
```

---

## Step 7: Expose Application

A NodePort Service was created.

Apply service:

```bash
kubectl apply -f service.yaml
```

Verify:

```bash
kubectl get svc
```

Application URL:

```
http://13.17.208.19:8000
```

---

# 🔄 Jenkins CI/CD Pipeline

Jenkins automates the complete deployment process.

Pipeline Stages:

1. Checkout Source Code
2. Build Docker Image
3. Push Docker Image to Registry
4. Deploy to Kubernetes Cluster
5. Verify Deployment

---

# Jenkins Pipeline Flow

```text
Git Push
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Trigger
    │
    ▼
Checkout Code
    │
    ▼
Build Docker Image
    │
    ▼
Push Image to Docker Registry
    │
    ▼
Deploy to Kubernetes
    │
    ▼
Update Deployment
    │
    ▼
Pods Created
    │
    ▼
Expose via NodePort
    │
    ▼
Application Available
```

---

# 🔥 CI/CD Workflow

Whenever code is pushed to GitHub:

- Jenkins automatically detects the changes.
- Pulls the latest source code.
- Builds a Docker image.
- Pushes the image to Docker Registry.
- Deploys the updated image to Kubernetes.
- Kubernetes performs a rolling update.
- Users immediately access the latest version.

---

# ☸ Kubernetes Components

## Deployment

Responsible for:

- Creating Pods
- Managing replicas
- Rolling updates
- Self-healing Pods

---

## Pods

Each Pod contains:

- RPS Game Container

Verify:

```bash
kubectl get pods
```

---

## Service

NodePort Service exposes the application externally.

Verify:

```bash
kubectl get svc
```

---

# 📊 Pipeline Architecture

```text
                  +----------------------+
                  |      Developer       |
                  +----------------------+
                            |
                         Git Push
                            |
                            ▼
                  +----------------------+
                  |       GitHub         |
                  +----------------------+
                            |
                            ▼
                  +----------------------+
                  |       Jenkins        |
                  |    CI/CD Pipeline    |
                  +----------------------+
                            |
          ----------------------------------------
          |                 |                    |
          ▼                 ▼                    ▼
 Checkout Code     Build Docker Image     Push Docker Image
                                                  |
                                                  ▼
                                        Docker Registry
                                                  |
                                                  ▼
                                      Kubernetes (Kind)
                                                  |
                                                  ▼
                                         Deployment Update
                                                  |
                                                  ▼
                                             Kubernetes Pods
                                                  |
                                                  ▼
                                           NodePort Service
                                                  |
                                                  ▼
                                             End Users
```

---

# 📋 Jenkins Pipeline Stages

| Stage | Description |
|--------|-------------|
| Checkout | Clone latest code from GitHub |
| Build | Build Docker image |
| Push | Push Docker image to Docker Registry |
| Deploy | Apply Kubernetes manifests |
| Verify | Verify Pods and Services |

---

# 📦 Kubernetes Resources

```
deployment.yaml

- Deployment
- ReplicaSet
- Pods
```

```
service.yaml

- NodePort Service
```

---

# 📈 Deployment Flow

```text
Developer
     │
Git Push
     │
GitHub
     │
Jenkins
     │
Docker Build
     │
Docker Push
     │
Docker Registry
     │
kubectl apply
     │
Deployment
     │
Pods
     │
NodePort
     │
Browser
```

---

# ✅ Verification Commands

Check cluster

```bash
kubectl cluster-info
```

Check nodes

```bash
kubectl get nodes
```

Check deployments

```bash
kubectl get deployments
```

Check pods

```bash
kubectl get pods
```

Check services

```bash
kubectl get svc
```

Describe deployment

```bash
kubectl describe deployment rps-game
```

View logs

```bash
kubectl logs rps-p1
```
---

# 🚀 Project Outcome

Successfully implemented an automated CI/CD pipeline that:

- ✔ Detects every GitHub push automatically.
- ✔ Builds a Docker image for the application.
- ✔ Pushes the image to Docker Registry.
- ✔ Deploys the latest image to a Kubernetes cluster created using Kind.
- ✔ Exposes the application using a NodePort Service.
- ✔ Eliminates manual deployment tasks.
- ✔ Provides a repeatable and reliable deployment process.

---

# 💡 Key Learnings

Through this project, I gained hands-on experience with:

- CI/CD Pipeline Development
- Jenkins Pipeline Automation
- Docker Containerization
- Docker Image Management
- Docker Registry Integration
- Kubernetes Deployments
- Kubernetes Services
- Kind Cluster Setup
- AWS EC2 Administration
- Git & GitHub Workflow
- Automated Application Deployment

---

# 👨‍💻 Author

**Jeevika**

DevOps Engineer

### Skills Demonstrated

- Jenkins
- Docker
- Docker Registry
- Kubernetes
- Kind
- AWS EC2
- Git & GitHub
- CI/CD
- Linux
- DevOps Automation

---

This project demonstrates a complete DevOps workflow by integrating GitHub, Jenkins, Docker, Docker Registry, Kubernetes, and AWS EC2 into a fully automated CI/CD pipeline. Every code push initiates an automated sequence that builds, packages, and deploys the application with minimal manual intervention. The project highlights best practices in continuous integration, continuous deployment, containerization, and Kubernetes orchestration, providing a solid foundation for deploying cloud-native applications.
````
