# ☸️ YumCart Deployment (Kubernetes + ArgoCD + Monitoring)

This repository contains **Kubernetes manifests and Helm charts** used to deploy the **YumCart** application on a Kubernetes cluster, integrated with **ArgoCD** for GitOps and basic monitoring using **Prometheus & Grafana**.

---

## 🚀 Deployment Flow

**1. CI/CD (in first repo):**
Jenkins builds the Docker image, pushes it to DockerHub, and automatically updates the Helm `values.yaml` file here.

**2. GitOps (this repo):**
ArgoCD watches this repository.  
Whenever a change is pushed (new image tag, configuration, etc.), ArgoCD automatically syncs and deploys the updated version to Kubernetes.

**3. Monitoring:**
Prometheus collects cluster metrics and Grafana visualizes them using imported dashboards.

---
      ┌─────────────────────────┐
      │       Developer         │
      │ (Push code to GitHub)   │
      └────────────┬────────────┘
                   │
                   ▼
      ┌─────────────────────────┐
      │        Jenkins CI        │
      │ Builds Docker image,     │
      │ Runs tests & scans,      │
      │ Pushes image to DockerHub│
      │ Updates values.yaml in   │
      │ yum-cart-deployment repo │
      └────────────┬────────────┘
                   │
                   ▼
      ┌─────────────────────────┐
      │        ArgoCD           │
      │ Detects Git changes     │
      │ Syncs app to cluster    │
      └────────────┬────────────┘
                   │
                   ▼
      ┌─────────────────────────┐
      │      Kubernetes         │
      │ Deploys app via Helm    │
      │ Exposes via Ingress     │
      └────────────┬────────────┘
                   │
                   ▼
      ┌─────────────────────────┐
      │  Prometheus & Grafana   │
      │  Monitor metrics & logs │
      └─────────────────────────┘


## 🧩 Components

| Component | Description |
|------------|--------------|
| **Helm** | Package manager for Kubernetes to manage app deployment |
| **ArgoCD** | Automates continuous delivery through GitOps |
| **Prometheus** | Metrics collection and alerting |
| **Grafana** | Visual dashboards for metrics |
| **Kubernetes** | Orchestrates and manages application containers |

---
