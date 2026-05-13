# Kubernetes Delivery Platform 🚀

Production-grade cloud-native delivery platform built on Kubernetes and AWS.

This project demonstrates how modern engineering teams build, deploy, secure, and observe scalable applications using production-focused DevOps and platform engineering practices.

Designed and built by Ogaji Igwe Samuel.

<img width="1536" height="1024" alt="DevOps architecture" src="https://github.com/user-attachments/assets/b7978578-0bb6-4468-905b-2f493447f988" />


---

# Project Overview

`kubernetes-delivery-platform` is a production-style Kubernetes platform running on Amazon EKS with automated CI/CD, service mesh security, canary deployments, and full-stack observability.

The platform simulates a real-world engineering environment where deployments are automated, services are secured with mTLS, traffic is intelligently managed, and operational visibility is built into the infrastructure from day one.

---

# Key Features

✅ Amazon EKS Kubernetes Cluster  
✅ GitHub Actions CI/CD Automation  
✅ Dockerized Application Deployment  
✅ Helm-based Kubernetes Packaging  
✅ Istio Service Mesh with mTLS  
✅ Canary Deployments with Traffic Splitting  
✅ Prometheus Metrics Collection  
✅ Grafana Dashboards & Visualization  
✅ Alertmanager Integration with Slack  
✅ Production-style Kubernetes Architecture  

---

# Architecture Overview

```text
Developer (git push)
        ↓
GitHub Actions CI/CD Pipeline
        ↓
Build Docker Image
        ↓
Push Image → Amazon ECR
        ↓
Helm Deployment
        ↓
Amazon EKS Cluster
 ├── Application Pods
 ├── Istio Service Mesh
 │     ├── mTLS Encryption
 │     ├── Traffic Routing
 │     └── Canary Releases
 │
 └── Observability Stack
       ├── Prometheus
       ├── Grafana
       └── Alertmanager → Slack
```

---

# Platform Architecture

## CI/CD Pipeline

The deployment workflow is fully automated using GitHub Actions.

### Pipeline Flow

```text
git push
   ↓
GitHub Actions
   ↓
Docker Build
   ↓
Push to Amazon ECR
   ↓
Helm Upgrade / Install
   ↓
Deploy to Amazon EKS
   ↓
Health Verification
```

The pipeline eliminates manual deployments and ensures repeatable infrastructure delivery.

---

# Infrastructure Stack

| Category | Technology |
|---|---|
| Cloud Platform | AWS |
| Kubernetes | Amazon EKS |
| Containerization | Docker |
| CI/CD | GitHub Actions |
| Package Management | Helm |
| Service Mesh | Istio |
| Monitoring | Prometheus |
| Visualization | Grafana |
| Alerting | Alertmanager + Slack |
| Container Registry | Amazon ECR |
| CLI Tooling | kubectl, eksctl, AWS CLI |

---

# Kubernetes & Service Mesh

The platform uses Amazon EKS for orchestration and Istio for advanced traffic management and service-to-service security.

## Implemented Features

- Kubernetes deployments and services
- Helm-based application packaging
- Automatic Istio sidecar injection
- STRICT mTLS encryption
- VirtualService traffic routing
- Canary deployments with traffic splitting
- Scalable container workloads

---

# Observability Stack

Operational visibility is a core part of the platform architecture.

## Monitoring

### Prometheus
- Metrics collection
- Service discovery
- Alert rules

### Grafana
- Real-time dashboards
- Infrastructure visualization
- Kubernetes metrics analysis

### Alertmanager
- Alert routing
- Notification grouping
- Slack integration

---

# Alerts Configured

The platform includes operational alerts for:

- High CPU usage
- High memory utilization
- Pod restarts
- Kubernetes health degradation
- Application availability issues

---

# Repository Structure

```text
kubernetes-delivery-platform/
│
├── app/
│   ├── index.html
│   └── Dockerfile
│
├── kubernetes-delivery-chart/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       ├── deployment.yaml
│       └── service.yaml
│
├── istio/
│   ├── gateway.yaml
│   ├── virtualservice.yaml
│   └── destinationrule.yaml
│
├── monitoring/
│   ├── prometheus/
│   ├── grafana/
│   └── alertmanager/
│
├── .github/workflows/
│   └── deploy.yaml
│
└── README.md
```

---

# Deployment Guide

## 1. Configure AWS

```bash
aws configure
```

---

## 2. Create EKS Cluster

```bash
eksctl create cluster \
  --name kubernetes-delivery-cluster \
  --region eu-north-1 \
  --nodegroup-name platform-nodes \
  --node-type t3.medium \
  --nodes 2 \
  --nodes-min 1 \
  --nodes-max 3 \
  --managed
```

---

## 3. Build Docker Image

```bash
docker build -t kubernetes-delivery-platform:v1.0 ./app
```

---

## 4. Push Image to Amazon ECR

```bash
docker push <ECR_URL>
```

---

## 5. Deploy with Helm

```bash
helm install kubernetes-delivery ./kubernetes-delivery-chart
```

---

# CI/CD Workflow

```text
Code Commit
    ↓
GitHub Actions Pipeline
    ↓
Container Build
    ↓
Amazon ECR Push
    ↓
Helm Deployment
    ↓
Amazon EKS Rollout
    ↓
Istio Traffic Routing
    ↓
Prometheus Monitoring
    ↓
Alertmanager Notifications
```

---

# Security Features

The platform includes multiple production-style security controls:

- mTLS encryption via Istio
- Kubernetes network isolation
- Private container registry (ECR)
- IAM-based AWS authentication
- Kubernetes secrets management
- Controlled ingress traffic

---

# Project Outcomes

This project successfully demonstrates:

✅ Production-grade Kubernetes operations  
✅ Automated cloud-native deployments  
✅ Secure service-to-service communication  
✅ Canary deployment strategies  
✅ Real-time monitoring and observability  
✅ Infrastructure scalability and resilience  

---

# Key Learnings

- Kubernetes enables scalable production systems
- CI/CD automation reduces deployment risk
- Observability is critical for reliability
- Service mesh improves traffic control and security
- Platform engineering requires operational thinking
- Debugging distributed systems is an essential skill

---

# Future Improvements

Planned enhancements include:

- Terraform infrastructure provisioning
- GitOps with ArgoCD
- Horizontal Pod Autoscaler (HPA)
- Distributed tracing with Jaeger
- Multi-environment deployments
- Policy enforcement with OPA/Gatekeeper

---

# Author

## 👨‍💻 Ogaji Igwe Samuel

GitHub: https://github.com/samklin92

LinkedIn: https://linkedin.com/in/samklin92

Repository: https://github.com/samklin92/kubernetes-delivery-platform.git

---

# Final Note

This project was built to simulate how modern cloud platforms are engineered in real production environments — combining automation, security, scalability, observability, and operational reliability into a single Kubernetes delivery platform.
