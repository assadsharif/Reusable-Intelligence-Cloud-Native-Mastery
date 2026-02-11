---
id: 001
title: Create FastAPI Dapr Agent Skill
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: asad
command: create skill
labels: ["fastapi", "dapr", "openai-agents-sdk", "skill", "scaffold", "cloud-native"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - .claude/skills/fastapi-dapr-agent/SKILL.md
  - .claude/skills/fastapi-dapr-agent/scripts/scaffold.py
  - .claude/skills/fastapi-dapr-agent/scripts/init_dapr.sh
tests:
  - none
---

## Prompt

Create the fastapi-dapr-agent skill at this path: /mnt/c/Users/HomePC/Desktop/CODE/Hackathon III_ Reusable Intelligence and Cloud-Native Mastery/.claude/skills/fastapi-dapr-agent/

Create these files:

1. SKILL.md — Purpose: Scaffold FastAPI + Dapr microservices with OpenAI Agents SDK integration. Follow the MCP Code Execution pattern (SKILL.md ~100 tokens -> scripts execute -> only results enter context).

Include:
- Frontmatter with name: fastapi-dapr-agent, description
- Scope section (Does/Does NOT)
- Tool Map table: scaffold.py (scaffold new service), init_dapr.sh (initialize Dapr components)
- Execution Pattern section
- Default Dapr config (state store: Redis, pub/sub: Redis or Kafka, service invocation: HTTP)
- Clarification Triggers (service name, agents list, pub/sub type)
- Must Follow / Must Avoid checklists
- Cross-Platform Compatibility with Goose recipe

2. scripts/scaffold.py — Python script that:
- Takes --name, --port (default 8000), --agents (comma-separated agent names), --output-dir args
- Creates a FastAPI service directory with:
  - main.py (FastAPI app with Dapr pub/sub subscription endpoint, health check)
  - agents/ directory with one file per agent (each agent is a class with name, instructions, model fields)
  - dapr/ directory with components/ (statestore.yaml, pubsub.yaml) and config.yaml
  - Dockerfile (Python 3.12-slim, installs deps, runs uvicorn)
  - requirements.txt (fastapi, uvicorn, dapr, openai-agents-sdk, httpx)
- Prints summary of created files

3. scripts/init_dapr.sh — Shell script that:
- Takes service-name and optional --namespace flag
- Checks if Dapr is installed (dapr --version), suggests install if missing
- Applies Dapr component YAMLs to Kubernetes (kubectl apply)
- Verifies Dapr sidecar injector is running

Make sure all scripts have shebangs, Python scripts use argparse.

## Response snapshot

Created the complete fastapi-dapr-agent skill with 3 files following existing project conventions (k8s-foundation, kafka-k8s-setup patterns). SKILL.md is ~100 tokens for the MCP Code Execution pattern. scaffold.py generates a full service directory tree (main.py, agents/, dapr/components/, Dockerfile, requirements.txt). init_dapr.sh checks Dapr/kubectl prerequisites and applies component YAMLs to Kubernetes with sidecar injector verification.

## Outcome

- Impact: New skill added to the agent skill library enabling FastAPI + Dapr + OpenAI Agents SDK microservice scaffolding
- Tests: none
- Files: 3 files created (SKILL.md, scripts/scaffold.py, scripts/init_dapr.sh)
- Next prompts: Run scaffold.py to test output, create a sample microservice, integrate with helm-packaging skill
- Reflection: Followed existing skill conventions from k8s-foundation and kafka-k8s-setup for consistency

## Evaluation notes (flywheel)

- Failure modes observed: none
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Test scaffold.py end-to-end with a sample service name
