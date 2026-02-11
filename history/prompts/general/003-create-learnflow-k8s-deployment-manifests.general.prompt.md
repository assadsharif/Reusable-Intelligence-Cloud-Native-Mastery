---
id: 003
title: Create LearnFlow K8s Deployment Manifests
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: asad
command: direct prompt
labels: ["kubernetes", "helm", "k8s", "learnflow", "deployment", "dapr", "ingress", "minikube"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/namespace.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/backend-deployment.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/backend-service.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/frontend-deployment.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/frontend-service.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/secrets.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/dapr-pubsub.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/dapr-statestore.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/base/kong-ingress.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/charts/Chart.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/charts/values.yaml
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/deploy.sh
tests:
  - none
---

## Prompt

Create Kubernetes deployment manifests and Helm charts for the LearnFlow application in /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/k8s/

The k8s/charts/ and k8s/base/ directories already exist.

Create ALL of the following files using the Write tool (do NOT use Bash for file creation):

1. k8s/base/namespace.yaml - Namespace definition for learnflow
2. k8s/base/backend-deployment.yaml - Backend Deployment with Dapr annotations
3. k8s/base/backend-service.yaml - Backend ClusterIP Service
4. k8s/base/frontend-deployment.yaml - Frontend Deployment
5. k8s/base/frontend-service.yaml - Frontend NodePort Service
6. k8s/base/secrets.yaml - Opaque Secret for API keys
7. k8s/base/dapr-pubsub.yaml - Dapr Kafka pub/sub Component
8. k8s/base/dapr-statestore.yaml - Dapr PostgreSQL state store Component
9. k8s/base/kong-ingress.yaml - Ingress routing /api to backend and / to frontend
10. k8s/charts/Chart.yaml - Helm chart metadata with Bitnami PostgreSQL and Kafka dependencies
11. k8s/charts/values.yaml - Helm chart values for backend, frontend, Dapr, and ingress
12. k8s/deploy.sh - Bash deployment script for Minikube

## Response snapshot

All 12 files created successfully using the Write tool in a single parallel batch. The Kubernetes manifests implement:
- Dedicated `learnflow` namespace with app label
- Backend Deployment with Dapr sidecar annotations (app-id, port, protocol), OPENAI_API_KEY from Secret, DATABASE_URL and KAFKA_BOOTSTRAP_SERVERS environment variables, resource limits (500m CPU / 512Mi memory), and health probes on /api/v1/health
- Frontend Deployment with NEXT_PUBLIC_API_URL pointing to backend service, resource limits (300m CPU / 256Mi memory), and liveness probe on /
- Backend ClusterIP Service on port 8000, Frontend NodePort Service on port 3000 (nodePort 30300)
- Kubernetes Secret for openai-api-key (placeholder value)
- Dapr Components for Kafka pub/sub and PostgreSQL state store
- Ingress routing learnflow.local /api to backend and / to frontend
- Helm Chart.yaml with Bitnami PostgreSQL (16.x.x) and Kafka (31.x.x) as optional dependencies
- Helm values.yaml with subchart overrides disabled (using external skills instead)
- deploy.sh script that builds Docker images in Minikube's Docker daemon, applies all manifests in order, conditionally applies Dapr components, and reports service URLs

## Outcome

- Impact: Complete K8s deployment infrastructure for LearnFlow platform, enabling Minikube-based local development
- Tests: none
- Files: 12 files created across k8s/base/, k8s/charts/, and k8s/ root
- Next prompts: Make deploy.sh executable, deploy to Minikube, add Helm templates for templated deployments, configure TLS for ingress
- Reflection: All files written in a single parallel Write batch for efficiency; deploy.sh needs chmod +x before execution

## Evaluation notes (flywheel)

- Failure modes observed: Bash was denied when attempting to chmod +x deploy.sh; user will need to run chmod manually
- Graders run and results (PASS/FAIL): N/A - no tests defined
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Add Helm templates under k8s/charts/templates/ to make the chart deployable via helm install
