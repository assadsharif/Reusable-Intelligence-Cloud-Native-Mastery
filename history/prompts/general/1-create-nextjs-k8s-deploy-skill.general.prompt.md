---
id: 1
title: Create nextjs-k8s-deploy Skill
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: asad
command: create skill
labels: ["skill", "nextjs", "kubernetes", "docker", "helm", "deployment"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - .claude/skills/nextjs-k8s-deploy/SKILL.md
  - .claude/skills/nextjs-k8s-deploy/scripts/build_and_deploy.sh
  - .claude/skills/nextjs-k8s-deploy/scripts/verify.py
  - .claude/skills/nextjs-k8s-deploy/templates/Dockerfile
tests:
  - none
---

## Prompt

Create the nextjs-k8s-deploy skill at this path: /mnt/c/Users/HomePC/Desktop/CODE/Hackathon III_ Reusable Intelligence and Cloud-Native Mastery/.claude/skills/nextjs-k8s-deploy/

Create these files:

1. SKILL.md — Purpose: Deploy Next.js apps on Kubernetes with Dockerfile + Helm chart. Follow MCP Code Execution pattern.

Include:
- Frontmatter with name: nextjs-k8s-deploy, description
- Scope section (Does/Does NOT)
- Tool Map: build_and_deploy.sh (build Docker image, deploy via Helm), verify.py (check pods/services)
- Execution Pattern section (MCP Code Execution)
- Clarification Triggers (app name, image tag, namespace, node port)
- Must Follow / Must Avoid checklists
- Cross-Platform Compatibility with Goose recipe

2. scripts/build_and_deploy.sh — Shell script that:
- Takes --app-name, --image-tag (default: latest), --namespace (default: default), --port (default: 3000) args
- Builds Docker image using Minikube's Docker daemon (eval $(minikube docker-env))
- Creates a simple Helm chart in /tmp with deployment.yaml, service.yaml, values.yaml
- Deploys via helm upgrade --install --wait
- Prints access URL (minikube service URL)

3. scripts/verify.py — Python script that:
- Takes --app-name, --namespace args
- Checks deployment replicas, pod status, service endpoints
- Outputs JSON health report
- Exits 0 if healthy, 1 if not

4. templates/Dockerfile — Multi-stage Dockerfile for Next.js:
- Stage 1: node:20-alpine, install deps, build
- Stage 2: node:20-alpine, copy standalone output, expose 3000, run with node server.js

Make sure all scripts have shebangs, Python scripts use argparse.

Write all files now.

## Response snapshot

Created the complete nextjs-k8s-deploy skill with 4 files following the project's MCP Code Execution pattern (Skills + Scripts). SKILL.md provides the agent-readable manifest (~100 tokens). build_and_deploy.sh handles Docker build via Minikube daemon and auto-generates a Helm chart in /tmp for deployment. verify.py checks deployment replicas, pod status, and service endpoints, outputting a JSON health report. templates/Dockerfile provides a multi-stage Next.js build (node:20-alpine, standalone output, non-root user).

## Outcome

- Impact: New skill added to the project's skill library, enabling automated Next.js deployment on Kubernetes via Minikube
- Tests: none (infrastructure/deployment skill — tested via actual deployment)
- Files: 4 files created (SKILL.md, build_and_deploy.sh, verify.py, Dockerfile)
- Next prompts: Test the skill by deploying a sample Next.js app, validate Helm chart rendering, add recipe.yaml for Goose compatibility
- Reflection: Followed established patterns from k8s-foundation and kafka-k8s-setup skills for consistency

## Evaluation notes (flywheel)

- Failure modes observed: none
- Graders run and results (PASS/FAIL): manual review PASS
- Prompt variant (if applicable): none
- Next experiment (smallest change to try): Add --dry-run flag to build_and_deploy.sh for testing chart generation without deploying
