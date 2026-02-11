# GCP Cloud Deployment — LearnFlow on GKE

## Overview

LearnFlow is deployed on Google Kubernetes Engine (GKE) using the existing `todo-chatbot` cluster in `us-central1-a`. Docker images are stored in Google Artifact Registry.

**Live URL:** `http://34.56.83.182`

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   GKE Cluster (us-central1-a)           │
│                   2 nodes, K8s v1.33.5                  │
│                                                         │
│  ┌─────────────────── learnflow namespace ───────────┐  │
│  │                                                   │  │
│  │  ┌──────────────┐      ┌──────────────────────┐   │  │
│  │  │   Frontend   │      │      Backend         │   │  │
│  │  │  Next.js 14  │      │  FastAPI + Agents    │   │  │
│  │  │  LoadBalancer │─────▶│  ClusterIP :8000     │   │  │
│  │  │  :80 external│      │  6 AI Agents         │   │  │
│  │  └──────────────┘      └──────────┬───────────┘   │  │
│  └───────────────────────────────────┼───────────────┘  │
│                                      │                  │
│  ┌─── postgres namespace ──┐  ┌─── kafka namespace ──┐  │
│  │  PostgreSQL 18.1.0      │  │  Kafka 3.8.1 KRaft   │  │
│  │  (Bitnami Helm)         │  │  (Single broker)     │  │
│  │  5Gi PVC                │  │                      │  │
│  └─────────────────────────┘  └──────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

## GCP Resources

| Resource | Details |
|----------|---------|
| **Project** | `gen-lang-client-0174245278` |
| **Account** | `assadsharif786@gmail.com` |
| **GKE Cluster** | `todo-chatbot` — `us-central1-a` |
| **Nodes** | 2x e2-medium (Container-Optimized OS) |
| **K8s Version** | v1.33.5-gke.2172001 |
| **Artifact Registry** | `us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/` |

## Docker Images

| Image | Registry Path |
|-------|--------------|
| Backend | `us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/backend:latest` |
| Frontend | `us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/frontend:latest` |

## Kubernetes Resources

### Namespaces
- `learnflow` — Frontend + Backend
- `postgres` — PostgreSQL (Helm)
- `kafka` — Apache Kafka (KRaft mode)

### Services

| Service | Type | Port | External IP |
|---------|------|------|-------------|
| `learnflow-frontend` | LoadBalancer | 80 → 3000 | `34.56.83.182` |
| `learnflow-backend` | ClusterIP | 8000 | Internal only |
| `postgres-postgresql` | ClusterIP | 5432 | Internal only |
| `kafka` | ClusterIP | 9092 | Internal only |

### Backend Agents

The backend exposes 6 AI-powered agents via the `/api/v1/health` endpoint:

| Agent | Purpose |
|-------|---------|
| `triage` | Routes student queries to the right specialist agent |
| `concepts` | Explains Python concepts with examples |
| `code_review` | Reviews student code for quality and best practices |
| `debug` | Helps students debug Python errors |
| `exercise` | Generates practice exercises |
| `progress` | Tracks learning progress |

## Deployment Steps

### Prerequisites
```bash
gcloud auth login
gcloud config set project gen-lang-client-0174245278
gcloud container clusters get-credentials todo-chatbot --zone us-central1-a
gcloud auth configure-docker us-central1-docker.pkg.dev
```

### 1. Build and Push Images
```bash
# Backend
cd learnflow-app/backend
docker build -t us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/backend:latest .
docker push us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/backend:latest

# Frontend
cd ../frontend
docker build -t us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/frontend:latest .
docker push us-central1-docker.pkg.dev/gen-lang-client-0174245278/learnflow/frontend:latest
```

### 2. Create Namespaces
```bash
kubectl create namespace learnflow
kubectl create namespace postgres
kubectl create namespace kafka
```

### 3. Deploy Infrastructure
```bash
# PostgreSQL via Helm
helm install postgres oci://registry-1.docker.io/bitnamicharts/postgresql \
  --namespace postgres \
  --set auth.username=learnflow \
  --set auth.password=learnflow \
  --set auth.database=learnflow \
  --set primary.persistence.size=5Gi \
  --wait

# Kafka (KRaft mode)
kubectl apply -f k8s/base/kafka-deployment.yaml
```

### 4. Deploy Application
```bash
# Secrets
kubectl apply -f k8s/base/secrets.yaml

# Backend + Frontend (GKE overlay)
kubectl apply -f k8s/gke/backend-deployment.yaml
kubectl apply -f k8s/base/backend-service.yaml
kubectl apply -f k8s/gke/frontend-deployment.yaml
kubectl apply -f k8s/gke/frontend-service.yaml
```

### 5. Verify
```bash
# All pods running
kubectl get pods -n learnflow
kubectl get pods -n postgres
kubectl get pods -n kafka

# Get external IP
kubectl get svc -n learnflow learnflow-frontend

# Test backend health
kubectl exec -n learnflow $(kubectl get pods -n learnflow -l app=learnflow-backend -o jsonpath='{.items[0].metadata.name}') \
  -- python -c "import urllib.request; print(urllib.request.urlopen('http://localhost:8000/api/v1/health').read().decode())"
```

## K8s Manifest Structure

```
learnflow-app/k8s/
├── base/                    # Minikube (local dev)
│   ├── namespace.yaml
│   ├── secrets.yaml
│   ├── backend-deployment.yaml   # imagePullPolicy: Never
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml  # imagePullPolicy: Never
│   ├── frontend-service.yaml     # NodePort
│   ├── kafka-deployment.yaml
│   ├── dapr-pubsub.yaml
│   ├── dapr-statestore.yaml
│   └── kong-ingress.yaml
├── gke/                     # GCP (production)
│   ├── backend-deployment.yaml   # Artifact Registry images
│   ├── frontend-deployment.yaml  # Artifact Registry images
│   └── frontend-service.yaml     # LoadBalancer
└── charts/                  # Helm charts
```

## Troubleshooting

### Frontend SWC Build Error
Next.js on Alpine requires `@next/swc-linux-x64-musl`. The Dockerfile pre-installs it:
```dockerfile
RUN npm install @next/swc-linux-x64-musl
```

### Docker Push Auth Failure
```bash
gcloud auth configure-docker us-central1-docker.pkg.dev
```

### Pod CrashLoopBackOff
```bash
kubectl logs -n learnflow <pod-name> --previous
kubectl describe pod -n learnflow <pod-name>
```

### Database Connection Issues
Verify PostgreSQL DNS: `postgres-postgresql.postgres.svc.cluster.local:5432`
```bash
kubectl get svc -n postgres
```

## Cost Considerations

- GKE cluster: shared with `todo-chatbot` (no additional cluster cost)
- 2x e2-medium nodes (~$50/month)
- Artifact Registry: minimal storage (~500MB)
- LoadBalancer: ~$18/month
- Persistent disk (5Gi PostgreSQL): ~$1/month
