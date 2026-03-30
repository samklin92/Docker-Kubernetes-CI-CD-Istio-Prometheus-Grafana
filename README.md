markdown# 🚀 My Epick Book — Production DevOps Project on AWS



!\[AWS](https://img.shields.io/badge/AWS-EKS-orange)

!\[Kubernetes](https://img.shields.io/badge/Kubernetes-v1.34.4-blue)

!\[Helm](https://img.shields.io/badge/Helm-v4.1.3-green)

!\[Istio](https://img.shields.io/badge/Istio-v1.29.1-purple)

!\[CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-black)

!\[Prometheus](https://img.shields.io/badge/Monitoring-Prometheus-red)

!\[Grafana](https://img.shields.io/badge/Visualisation-Grafana-orange)



\---



\## 📌 Overview



A production-grade DevOps project built from scratch on AWS EKS.

This project demonstrates the full DevOps lifecycle —

from containerisation to deployment, CI/CD automation,

service mesh security, and production monitoring with custom alerts.



\---



\## 🏗️ Architecture

```

Developer (git push)

&#x20;       │

&#x20;       ▼

GitHub Repository

&#x20;       │

&#x20;       ▼

GitHub Actions CI/CD

&#x20; ├── Build Docker image

&#x20; ├── Push to Amazon ECR

&#x20; └── Deploy to EKS via Helm

&#x20;             │

&#x20;             ▼

&#x20;       AWS EKS Cluster (eu-north-1)

&#x20;       ├── Istio Service Mesh

&#x20;       │   ├── Envoy sidecars (mTLS)

&#x20;       │   ├── Istio Gateway

&#x20;       │   ├── VirtualService

&#x20;       │   └── Canary deployments (80/20)

&#x20;       │

&#x20;       ├── Application

&#x20;       │   ├── Helm Chart

&#x20;       │   ├── 2 x nginx Pods

&#x20;       │   └── AWS Elastic Load Balancer

&#x20;       │

&#x20;       └── Monitoring Stack

&#x20;           ├── Prometheus

&#x20;           ├── Grafana (public URL)

&#x20;           └── Alertmanager → Slack

```



\---



\## 🛠️ Tech Stack



| Technology | Purpose |

|-----------|---------|

| \*\*AWS EKS\*\* | Managed Kubernetes cluster |

| \*\*Amazon ECR\*\* | Private container registry |

| \*\*Docker\*\* | Application containerisation |

| \*\*Kubernetes\*\* | Container orchestration |

| \*\*Helm\*\* | Kubernetes package manager |

| \*\*GitHub Actions\*\* | CI/CD pipeline automation |

| \*\*Istio\*\* | Service mesh \& mTLS encryption |

| \*\*Prometheus\*\* | Metrics collection \& storage |

| \*\*Grafana\*\* | Metrics visualisation |

| \*\*Alertmanager\*\* | Alert routing to Slack |

| \*\*eksctl\*\* | EKS cluster provisioning |

| \*\*AWS CLI\*\* | AWS account management |



\---



\## 📁 Project Structure

```

my-epick-book/

├── app/

│   ├── index.html              ← Application source code

│   └── Dockerfile              ← Container image definition

│

├── epick-book-chart/           ← Helm Chart

│   ├── Chart.yaml              ← Chart metadata

│   ├── values.yaml             ← Configuration values

│   └── templates/

│       ├── deployment.yaml     ← Kubernetes Deployment

│       └── service.yaml        ← Kubernetes Service

│

├── .github/

│   └── workflows/

│       └── deploy.yaml         ← GitHub Actions CI/CD pipeline

│

└── README.md

```



\---



\## 🚀 Getting Started



\### Prerequisites

```bash

\# Install AWS CLI

winget install Amazon.AWSCLI



\# Install eksctl

winget install eksctl



\# Install Helm

winget install Helm.Helm



\# Verify installations

aws --version

eksctl version

helm version

```



\### Configure AWS

```bash

aws configure

\# Enter: Access Key, Secret Key, Region (eu-north-1), json

```



\### Create EKS Cluster

```bash

eksctl create cluster \\

\--name epick-book-cluster \\

\--region eu-north-1 \\

\--nodegroup-name epick-book-nodes \\

\--node-type t3.medium \\

\--nodes 2 \\

\--nodes-min 1 \\

\--nodes-max 3 \\

\--managed

```



\### Create ECR Repository

```bash

aws ecr create-repository \\

\--repository-name my-epick-book \\

\--region eu-north-1

```



\### Build \& Push to ECR

```bash

\# Login to ECR

aws ecr get-login-password --region eu-north-1 | \\

docker login --username AWS --password-stdin \\

109804294707.dkr.ecr.eu-north-1.amazonaws.com



\# Build \& Push

docker build -t my-epick-book:v1.0 ./app

docker tag my-epick-book:v1.0 \\

109804294707.dkr.ecr.eu-north-1.amazonaws.com/my-epick-book:v1.0

docker push \\

109804294707.dkr.ecr.eu-north-1.amazonaws.com/my-epick-book:v1.0

```



\### Deploy with Helm

```bash

helm install epick-book ./epick-book-chart

kubectl get pods

kubectl get svc

```



\---



\## 🔄 CI/CD Pipeline



The GitHub Actions pipeline triggers automatically on every push to `main`:

```

git push → Build Docker image → Push to ECR → Deploy to EKS → Verify

```



\### Required GitHub Secrets



| Secret | Description |

|--------|-------------|

| `AWS\_ACCESS\_KEY\_ID` | AWS access key |

| `AWS\_SECRET\_ACCESS\_KEY` | AWS secret key |

| `AWS\_REGION` | `eu-north-1` |

| `ECR\_REPOSITORY` | `my-epick-book` |

| `EKS\_CLUSTER\_NAME` | `epick-book-cluster` |



\---



\## 🕸️ Istio Service Mesh



\### Install Istio

```bash

curl -L https://istio.io/downloadIstio | sh -

cd istio-1.\*

export PATH=$PWD/bin:$PATH

istioctl install --set profile=demo -y

```



\### Enable Sidecar Injection

```bash

kubectl label namespace default istio-injection=enabled

kubectl rollout restart deployment/epick-book-epick-book

```



\### Enable mTLS STRICT Mode

```bash

kubectl apply -f - <<EOF

apiVersion: security.istio.io/v1beta1

kind: PeerAuthentication

metadata:

&#x20; name: default

&#x20; namespace: default

spec:

&#x20; mtls:

&#x20;   mode: STRICT

EOF

```



\### Canary Deployment (80/20 Split)

```bash

kubectl apply -f - <<EOF

apiVersion: networking.istio.io/v1alpha3

kind: VirtualService

metadata:

&#x20; name: epick-book-vs

spec:

&#x20; hosts:

&#x20;   - "\*"

&#x20; gateways:

&#x20;   - epick-book-gateway

&#x20; http:

&#x20;   - route:

&#x20;       - destination:

&#x20;           host: epick-book-epick-book-svc

&#x20;           port:

&#x20;             number: 80

&#x20;         weight: 80

&#x20;       - destination:

&#x20;           host: epick-book-epick-book-svc

&#x20;           port:

&#x20;             number: 80

&#x20;         weight: 20

EOF

```



\---



\## 📊 Monitoring \& Alerting



\### Install Prometheus \& Grafana

```bash

kubectl create namespace monitoring



helm repo add prometheus-community \\

https://prometheus-community.github.io/helm-charts

helm repo update



helm install monitoring \\

prometheus-community/kube-prometheus-stack \\

\--namespace monitoring \\

\--set grafana.service.type=LoadBalancer \\

\--set prometheus.service.type=LoadBalancer

```



\### Get Grafana Password

```bash

kubectl get secret monitoring-grafana \\

\-n monitoring \\

\-o jsonpath="{.data.admin-password}" | base64 --decode

```



\### Custom Alert Rules

```yaml

apiVersion: monitoring.coreos.com/v1

kind: PrometheusRule

metadata:

&#x20; name: epick-book-alerts

&#x20; namespace: monitoring

&#x20; labels:

&#x20;   release: monitoring

spec:

&#x20; groups:

&#x20;   - name: epick-book.rules

&#x20;     rules:

&#x20;       - alert: HighCPUUsage

&#x20;         expr: container\_cpu\_usage\_seconds\_total{container="epick-book"} > 0.8

&#x20;         for: 1m

&#x20;         labels:

&#x20;           severity: warning

&#x20;         annotations:

&#x20;           summary: "High CPU usage detected"



&#x20;       - alert: PodRestarting

&#x20;         expr: kube\_pod\_container\_status\_restarts\_total{namespace="default"} > 3

&#x20;         for: 1m

&#x20;         labels:

&#x20;           severity: critical

&#x20;         annotations:

&#x20;           summary: "Pod restarting too many times"



&#x20;       - alert: HighMemoryUsage

&#x20;         expr: container\_memory\_usage\_bytes{container="epick-book"} > 200000000

&#x20;         for: 1m

&#x20;         labels:

&#x20;           severity: warning

&#x20;         annotations:

&#x20;           summary: "High memory usage detected"

```



\---



\## ⚠️ Cleanup



To avoid AWS charges, delete all resources when done:

```bash

eksctl delete cluster \\

\--name epick-book-cluster \\

\--region eu-north-1

```



\---



\## 📈 Project Outcomes

```

✅ Production EKS cluster on AWS

✅ Private container registry (ECR)

✅ Zero-downtime deployments via Helm

✅ Fully automated CI/CD pipeline

✅ mTLS encryption via Istio

✅ Canary deployments (80/20 split)

✅ Real-time monitoring on Grafana

✅ Custom Slack alerts via Alertmanager

```



\---



\## 🧠 Key Learnings



\- EKS provisions a production Kubernetes cluster in minutes

\- Amazon ECR integrates natively with EKS for secure image storage

\- Helm bundles all Kubernetes resources into a single deployable package

\- GitHub Actions automates the entire build-push-deploy cycle

\- Istio injects Envoy sidecars automatically with zero app code changes

\- mTLS STRICT mode encrypts all service-to-service traffic automatically

\- Canary deployments enable safe production releases with traffic control

\- Prometheus pulls metrics every 15 seconds from all cluster components

\- Alertmanager routes alerts to Slack for instant team notification



\---



\## 👨‍💻 Author



\*\*Samuel Klin\*\*

\- GitHub: \[@samklin92](https://github.com/samklin92)

\- LinkedIn: \[samklin92](https://linkedin.com/in/samklin92)



\---



> 🚀 \*Built with passion. Deployed with confidence. Monitored with precision.\*



