---
id: 1
title: Create Docusaurus Deploy Skill
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: user
command: create skill
labels: ["docusaurus", "kubernetes", "deployment", "skill-creation", "cloud-native"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - .claude/skills/docusaurus-deploy/SKILL.md
  - .claude/skills/docusaurus-deploy/scripts/init_docs.sh
  - .claude/skills/docusaurus-deploy/scripts/deploy.sh
  - .claude/skills/docusaurus-deploy/scripts/verify.py
tests:
  - none
---

## Prompt

Create the docusaurus-deploy skill at this path: /mnt/c/Users/HomePC/Desktop/CODE/Hackathon III_ Reusable Intelligence and Cloud-Native Mastery/.claude/skills/docusaurus-deploy/

Create these files:

1. SKILL.md — Purpose: Deploy Docusaurus documentation sites on Kubernetes. Follow MCP Code Execution pattern.

Include:
- Frontmatter with name: docusaurus-deploy, description
- Scope (Does: initialize Docusaurus project, build static site, containerize, deploy to K8s / Does NOT: write documentation content, configure custom plugins)
- Tool Map: init_docs.sh (scaffold Docusaurus project), deploy.sh (build + containerize + deploy), verify.py (check deployment health)
- Execution Pattern section (MCP Code Execution)
- Clarification Triggers (project name, title, port, namespace)
- Must Follow / Must Avoid
- Cross-Platform Compatibility with Goose recipe

2. scripts/init_docs.sh — Shell script that:
- Takes --name (project name), --title (site title), --output-dir args
- Checks if npx is available
- Runs npx create-docusaurus to scaffold a new Docusaurus project (classic template)
- Adds a Dockerfile for the static site (nginx:alpine based, copies build output)
- Prints next steps

3. scripts/deploy.sh — Shell script that:
- Takes --name, --namespace (default: docs), --port (default: 3000) args
- Builds the Docusaurus site (npm run build)
- Builds Docker image using Minikube's Docker daemon
- Creates K8s deployment + service YAML (using heredoc, applies with kubectl)
- Waits for rollout
- Prints access URL

4. scripts/verify.py — Python script that:
- Takes --name, --namespace args
- Checks deployment, pods, and service status
- Outputs JSON health report
- Exits 0 if healthy, 1 if not

Make sure all scripts have shebangs and Python scripts use argparse.

Write all files now.

## Response snapshot

Created the complete docusaurus-deploy skill with 4 files following the established project patterns (matching k8s-foundation and kafka-k8s-setup conventions):

1. **SKILL.md** -- Full skill definition with frontmatter, scope, tool map, MCP Code Execution pattern, clarification triggers, must follow/avoid rules, and Goose recipe compatibility.
2. **scripts/init_docs.sh** -- Scaffolds Docusaurus project with classic template, adds multi-stage Dockerfile (node:18-alpine builder + nginx:alpine production), .dockerignore, and prints next steps.
3. **scripts/deploy.sh** -- Builds static site, builds Docker image via Minikube Docker daemon, applies K8s Deployment + NodePort Service with heredoc, waits for rollout, prints access URL.
4. **scripts/verify.py** -- Checks deployment, pods, and service status via kubectl JSON output, builds structured health report, resolves access URL via minikube ip, exits 0/1.

## Outcome

- Impact: New skill added to the project's skill library for deploying documentation sites on Kubernetes
- Tests: none
- Files: 4 files created (SKILL.md, init_docs.sh, deploy.sh, verify.py)
- Next prompts: Test the skill end-to-end on Minikube, add the skill to AGENTS.md
- Reflection: Followed existing kafka-k8s-setup and k8s-foundation patterns closely for consistency

## Evaluation notes (flywheel)

- Failure modes observed: none
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Add integration test that validates the full init -> deploy -> verify pipeline
