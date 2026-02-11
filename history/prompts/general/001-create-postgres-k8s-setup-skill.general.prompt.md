---
id: 001
title: Create PostgreSQL K8s Setup Skill
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: user
command: create skill
labels: ["postgres", "kubernetes", "helm", "skill", "infrastructure"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - .claude/skills/postgres-k8s-setup/SKILL.md
  - .claude/skills/postgres-k8s-setup/scripts/deploy.sh
  - .claude/skills/postgres-k8s-setup/scripts/verify.py
  - .claude/skills/postgres-k8s-setup/scripts/migrate.py
tests:
  - none
---

## Prompt

Create the postgres-k8s-setup skill at this path: /mnt/c/Users/HomePC/Desktop/CODE/Hackathon III_ Reusable Intelligence and Cloud-Native Mastery/.claude/skills/postgres-k8s-setup/

Create these files:

1. SKILL.md - Following the same pattern as the kafka-k8s-setup skill. Purpose: Deploy PostgreSQL on Kubernetes via Helm (Bitnami chart), run migrations, verify database readiness. Include Tool Map, Execution Pattern (MCP Code Execution), Cross-Platform Compatibility (Goose recipe).

2. scripts/deploy.sh - Shell script to deploy PostgreSQL via Bitnami Helm chart. Supports --namespace (default: postgres), --password, --database, --release flags. Uses helm upgrade --install with --wait. Creates namespace if needed. Sets persistence.size=2Gi for Minikube. Prints connection info at end.

3. scripts/verify.py - Python script to verify PostgreSQL pods and services. Checks pods in namespace, checks PVC status, outputs JSON health report.

4. scripts/migrate.py - Python script that takes --host, --port, --database, --user, --password, --sql-dir args. Runs .sql files from a directory in alphabetical order using psql via kubectl exec on the postgres pod. Reports which migrations ran.

Make sure all scripts are executable (have #!/usr/bin/env shebang), use argparse for Python scripts, and follow the MCP Code Execution pattern (scripts run externally, only results enter context).

Write all files now.

## Response snapshot

Created the complete postgres-k8s-setup skill with 4 files following the kafka-k8s-setup pattern:
- SKILL.md: Skill definition with Tool Map, Execution Pattern, Default Config, Clarification Triggers, Must Follow/Avoid, and Goose cross-platform recipe
- scripts/deploy.sh: Helm-based deployment with --namespace, --password, --database, --release flags, namespace creation, persistence.size=2Gi, --wait, connection info output
- scripts/verify.py: Checks pods, services, and PVCs; outputs JSON health report with healthy boolean
- scripts/migrate.py: Discovers .sql files alphabetically, executes via kubectl exec psql, stops on first failure, outputs JSON migration report

## Outcome

- Impact: New infrastructure skill for PostgreSQL K8s deployment, migration, and verification
- Tests: none (infrastructure scripts require live K8s cluster)
- Files: 4 files created under .claude/skills/postgres-k8s-setup/
- Next prompts: Test deployment on Minikube, create sample migration SQL files, integrate with application deployment workflow
- Reflection: Pattern matched kafka-k8s-setup closely; added PVC checks and migration support as PostgreSQL-specific features

## Evaluation notes (flywheel)

- Failure modes observed: none
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Run deploy.sh against a live Minikube to validate Helm values
