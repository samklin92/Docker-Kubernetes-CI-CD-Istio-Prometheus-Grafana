# 👨‍💻 Samuel Klin  
### 🚀 Production DevOps Platform on AWS — *My Epick Book*

---

## 🎯 Project Purpose

This project was designed and built by **Samuel Klin** to simulate a real-world production DevOps environment.

It demonstrates how modern engineering teams design, deploy, secure, and monitor applications at scale using cloud-native tools and best practices.

The goal of this project is to:

- Showcase end-to-end DevOps capabilities (build → deploy → monitor)  
- Demonstrate production-grade Kubernetes operations on AWS  
- Implement secure microservices communication using a service mesh  
- Automate deployments using CI/CD and GitOps principles  
- Provide full observability with monitoring and alerting  

---

## 🚀 TL;DR

A production-ready cloud platform featuring:

- Kubernetes cluster on Amazon EKS  
- CI/CD automation with GitHub Actions  
- Dockerized application deployed via Helm  
- Service mesh with Istio (mTLS enabled)  
- Canary deployments (traffic splitting)  
- Monitoring with Prometheus & Grafana  
- Alerting via Alertmanager → Slack  

---

## 🧰 Tech Stack

### ☁️ Cloud Platform
- AWS (EKS, ECR, IAM, VPC)

### ☸️ Container Orchestration
- Kubernetes (Amazon EKS)

### 📦 Containerization
- Docker

### 🔄 CI/CD & Automation
- GitHub Actions (pipeline automation)

### 📦 Package Management
- Helm (Kubernetes package manager)

### 🕸️ Service Mesh & Security
- Istio (mTLS, traffic routing, canary deployments)

### 📊 Monitoring & Observability
- Prometheus (metrics collection)  
- Grafana (visualization dashboards)  
- Alertmanager (alert routing to Slack)  

### 🛠️ CLI & Tooling
- AWS CLI  
- eksctl  
- kubectl  

---

## 🏗️ Architecture Overview

# 👨‍💻 Samuel Klin  
### 🚀 Production DevOps Platform on AWS — *My Epick Book*

---

## 🎯 Project Purpose

This project was designed and built by **Samuel Klin** to simulate a real-world production DevOps environment.

It demonstrates how modern engineering teams design, deploy, secure, and monitor applications at scale using cloud-native tools and best practices.

The goal of this project is to:

- Showcase end-to-end DevOps capabilities (build → deploy → monitor)  
- Demonstrate production-grade Kubernetes operations on AWS  
- Implement secure microservices communication using a service mesh  
- Automate deployments using CI/CD and GitOps principles  
- Provide full observability with monitoring and alerting  

---

## 🚀 TL;DR

A production-ready cloud platform featuring:

- Kubernetes cluster on Amazon EKS  
- CI/CD automation with GitHub Actions  
- Dockerized application deployed via Helm  
- Service mesh with Istio (mTLS enabled)  
- Canary deployments (traffic splitting)  
- Monitoring with Prometheus & Grafana  
- Alerting via Alertmanager → Slack  

---

## 🧰 Tech Stack

### ☁️ Cloud Platform
- AWS (EKS, ECR, IAM, VPC)

### ☸️ Container Orchestration
- Kubernetes (Amazon EKS)

### 📦 Containerization
- Docker

### 🔄 CI/CD & Automation
- GitHub Actions (pipeline automation)

### 📦 Package Management
- Helm (Kubernetes package manager)

### 🕸️ Service Mesh & Security
- Istio (mTLS, traffic routing, canary deployments)

### 📊 Monitoring & Observability
- Prometheus (metrics collection)  
- Grafana (visualization dashboards)  
- Alertmanager (alert routing to Slack)  

### 🛠️ CLI & Tooling
- AWS CLI  
- eksctl  
- kubectl  

---

## 🏗️ Architecture Overview
Developer (git push)
↓
GitHub Actions CI/CD
↓
Build → Push (ECR) → Deploy (Helm)
↓
Amazon EKS Cluster
├── Application Pods (nginx)
├── Istio Service Mesh (mTLS + traffic control)
└── Monitoring Stack (Prometheus + Grafana + Alertmanager)

---

## 🧱 Core Components

### ☁️ Cloud Infrastructure
- Amazon EKS cluster deployed in AWS  
- Amazon ECR for container image storage  

---

### 🔄 CI/CD Pipeline
- Automated build and deployment pipeline:
  - Build Docker image  
  - Push to ECR  
  - Deploy to EKS using Helm  

---

### ☸️ Kubernetes Deployment
- Helm chart for application deployment  
- Scalable nginx-based application  
- Kubernetes services exposed via LoadBalancer  

---

### 🕸️ Service Mesh (Istio)
- Automatic sidecar injection (Envoy proxies)  
- mTLS encryption in STRICT mode  
- Traffic routing using VirtualService  
- Canary deployments with traffic splitting  

---

### 📊 Monitoring & Alerting
- Prometheus for metrics collection  
- Grafana dashboards for visualization  
- Alertmanager integrated with Slack  
- Custom alerts for CPU, memory, and pod health  

---

## 📁 Project Structure
my-epick-book/
├── app/ # Application source code
│ ├── index.html
│ └── Dockerfile
│
├── epick-book-chart/ # Helm chart
│ ├── Chart.yaml
│ ├── values.yaml
│ └── templates/
│ ├── deployment.yaml
│ └── service.yaml
│
├── .github/workflows/ # CI/CD pipeline
│ └── deploy.yaml
│
└── README.md

---

## 🚀 Deployment Workflow

1. Configure AWS  

aws configure


2. Create EKS cluster  

eksctl create cluster
--name epick-book-cluster
--region eu-north-1
--nodegroup-name epick-book-nodes
--node-type t3.medium
--nodes 2
--nodes-min 1
--nodes-max 3
--managed


3. Build & push Docker image  

docker build -t my-epick-book:v1.0 ./app
docker push <ECR_URL>


4. Deploy with Helm  

helm install epick-book ./epick-book-chart


---

## 🔄 CI/CD Workflow


git push → build → push → deploy → verify


---

## 📊 Monitoring & Alerts

- Real-time metrics via Prometheus  
- Grafana dashboards for visualization  
- Alerts triggered for:
  - High CPU usage  
  - High memory usage  
  - Pod restarts  

---

## 🧹 Cleanup


eksctl delete cluster
--name epick-book-cluster
--region eu-north-1


---

## 📈 Project Outcomes

- Production-ready Kubernetes platform on AWS  
- Fully automated CI/CD pipeline  
- Secure service-to-service communication (mTLS)  
- Canary deployments with traffic control  
- Real-time monitoring and alerting  

---

## 🧠 Key Learnings

- Kubernetes enables scalable production systems  
- CI/CD removes manual deployment risks  
- Service mesh enhances security and traffic control  
- Observability is essential for reliability  
- Debugging is a critical DevOps skill  

---

## 👨‍💻 Author

**Ogaji Igwe Samuel**  
- GitHub: https://github.com/samklin92  
- LinkedIn: https://linkedin.com/in/samklin92  
