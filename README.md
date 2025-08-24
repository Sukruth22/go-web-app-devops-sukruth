# Go Web App — DevOps Project 🚀

A complete DevOps pipeline for a simple Go web application, demonstrating:

- ✅ Containerization with **multi-stage Docker builds**  
- ✅ Deployment to **Kubernetes** with Helm  
- ✅ Continuous Integration with **GitHub Actions**  
- ✅ Continuous Delivery with **Argo CD (GitOps)**  
- ✅ **Ingress** exposure via NGINX and nip.io  
- ✅ Runs locally on **Minikube** (Docker Desktop)  

---

## 📖 Project Overview

This project takes a basic Go web app (serving static HTML pages) and runs it through a **full production-style DevOps workflow**.  

**Flow:**
1. Developer pushes code → GitHub Actions builds & pushes image to GHCR.  
2. Workflow bumps the Helm `values-dev.yaml` image tag.  
3. Argo CD detects Git changes and syncs Helm release to Kubernetes.  
4. App becomes available via Ingress at `http://go-web-app.127.0.0.1.nip.io/home`.

---

## 🏗 Architecture

[ GitHub Repo ] --push--> [ GitHub Actions CI ]
| |
| (Docker Build) v
|-----------------> [ GHCR Registry ]
|
[ Argo CD (GitOps) ]
|
[ Kubernetes (Minikube) ]
|
[ Helm Chart Deployment ]
|
http://go-web-app.127.0.0.1.nip.io

yaml
Copy
Edit

---

## ⚡️ Tech Stack

- **Go 1.22** (web app)  
- **Docker / GHCR** (container registry)  
- **Kubernetes (Minikube)** (runtime)  
- **Helm** (templated manifests, multi-env)  
- **GitHub Actions** (CI)  
- **Argo CD** (CD / GitOps)  
- **Ingress NGINX + nip.io** (routing)

---

## 🛠 Setup Instructions

### 1. Clone repos
```bash
git clone https://github.com/Sukruth22/go-web-app-devops-sukruth.git
cd go-web-app-devops-sukruth
2. Build & run locally (optional)
bash
Copy
Edit
docker build -f docker/Dockerfile -t go-web-app:dev .
docker run --rm -p 8080:8080 go-web-app:dev
curl -i http://localhost:8080/home
3. Start Minikube
bash
Copy
Edit
minikube start --driver=docker --cpus=2 --memory=3000
minikube addons enable ingress
minikube tunnel   # keep this open
4. Deploy with Helm
bash
Copy
Edit
helm upgrade --install go-web-app ./helm/go-web-app \
  -f helm/go-web-app/env/values-dev.yaml \
  --namespace go-web-app --create-namespace
5. Access the app
bash
Copy
Edit
curl -i http://go-web-app.127.0.0.1.nip.io/home
🔄 CI/CD Flow
CI (GitHub Actions):

Runs tests (go test)

Builds Docker image

Pushes to GHCR (ghcr.io/sukruth22/go-web-app)

Auto-bumps Helm dev values with new image tag

CD (Argo CD):

Watches this repo (helm/go-web-app)

Syncs to Kubernetes on every change

Automates rollout with self-healing & pruning

🌱 Future Enhancements
Add TLS with cert-manager + Let’s Encrypt

Add Prometheus & Grafana monitoring

Add prod environment with manual promotion

Autoscaling demo with load tests

✨ Credits
Original app: iam-veeramalla/go-web-app

DevOps workflow: built by Sukruth R
