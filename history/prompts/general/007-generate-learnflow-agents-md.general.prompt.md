---
id: 007
title: Generate LearnFlow AGENTS.md
stage: general
date: 2026-02-12
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: assadsharif
command: generate AGENTS.md
labels: ["agents-md", "learnflow", "documentation", "codebase-scan"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - /mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/AGENTS.md
tests:
  - none
---

## Prompt

Generate an AGENTS.md file for the LearnFlow application repository at "/mnt/c/Users/HomePC/Desktop/CODE/learnflow-app".

This repo is "LearnFlow" — an AI-powered Python tutoring platform built using reusable skills. Scan the codebase to discover:
1. Backend structure in `backend/` (FastAPI + AI agents)
2. Frontend structure in `frontend/` (Next.js)
3. Documentation site in `docs/` (Docusaurus)
4. Kubernetes manifests in `k8s/base/` (Minikube) and `k8s/gke/` (GKE)
5. Argo CD config in `k8s/argocd/`
6. GitHub Actions workflows in `.github/workflows/`
7. Helm charts if any
8. Any agent definitions (the backend has 6 AI agents: Triage, Concepts, Code Review, Debug, Exercise, Progress)

Then create a comprehensive AGENTS.md at the repo root with:
- Project overview (AI-powered Python tutoring platform)
- GitHub: github.com/assadsharif/learnflow-app
- AI Agents section (the 6 tutoring agents and what they do)
- Architecture (Frontend -> Backend -> Kafka -> PostgreSQL)
- Cloud deployment info (GKE cluster, Artifact Registry, Argo CD GitOps)
- Live endpoints: Frontend http://34.56.83.182, Docs http://34.122.229.139, Argo CD https://34.44.123.161
- CI/CD pipeline (GitHub Actions + Argo CD)
- Key directory structure
- Built using Skills from the companion skills-library repo

Write the AGENTS.md file to the repo root. Make it comprehensive but well-organized.

## Response snapshot

Scanned the entire learnflow-app codebase across all directories (backend, frontend, docs, k8s, .github). Read all 6 agent definition files, the orchestrator, routes, schemas, config, Dockerfiles, K8s manifests (base + GKE + ArgoCD), Helm charts, CI/CD workflows, frontend components, and docs config. Created a comprehensive AGENTS.md at `/mnt/c/Users/HomePC/Desktop/CODE/learnflow-app/AGENTS.md` with sections for: project overview, all 6 AI agents with pipeline diagram, full architecture diagram with technology stack, API endpoints, data models, database schema, GKE cloud deployment details, live endpoints, CI/CD pipeline (GitHub Actions + Argo CD GitOps flow), local development guide, complete directory tree, skills attribution, environment variables, and K8s resource budgets.

## Outcome

- Impact: Created comprehensive AGENTS.md documenting the full LearnFlow platform for agent and human consumption
- Tests: none
- Files: 1 file created (AGENTS.md)
- Next prompts: Commit the AGENTS.md, review for accuracy
- Reflection: Thorough codebase scan ensured accurate representation of all components

## Evaluation notes (flywheel)

- Failure modes observed: none
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): N/A
