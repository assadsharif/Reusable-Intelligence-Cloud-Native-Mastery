# AGENTS.md

> **Reusable Intelligence & Cloud-Native Mastery** -- Portable AI agent skills with the MCP Code Execution pattern.
>
> GitHub: [assadsharif/Reusable-Intelligence-Cloud-Native-Mastery](https://github.com/assadsharif/Reusable-Intelligence-Cloud-Native-Mastery)
>
> Generated: 2026-02-12

---

## Table of Contents

- [Project Overview](#project-overview)
- [The Skills + Code Execution Pattern](#the-skills--code-execution-pattern)
- [Cross-Platform Compatibility](#cross-platform-compatibility)
- [Inventory Summary](#inventory-summary)
- [Skills Reference](#skills-reference)
  - [Cloud-Native & Kubernetes](#cloud-native--kubernetes)
  - [Backend & API Development](#backend--api-development)
  - [Frontend & UI](#frontend--ui)
  - [AI & Agent Frameworks](#ai--agent-frameworks)
  - [MCP Tooling & Protocol](#mcp-tooling--protocol)
  - [Testing & Quality](#testing--quality)
  - [DevOps & CI/CD](#devops--cicd)
  - [Document & Media Processing](#document--media-processing)
  - [Skill Lifecycle (Meta)](#skill-lifecycle-meta)
  - [FTE Orchestration Suite](#fte-orchestration-suite)
  - [Utility & Infrastructure](#utility--infrastructure)
- [MCP Servers](#mcp-servers)
  - [Registered Servers (22)](#registered-servers-22)
  - [Additional Server Implementations (6)](#additional-server-implementations-6)
- [CI/CD Pipeline](#cicd-pipeline)
- [Directory Structure](#directory-structure)
- [Constitution & Governance](#constitution--governance)

---

## Project Overview

This repository is a **skills library** -- a curated collection of 55 portable AI agent skills, 28 MCP server implementations, and 77 executable scripts. Its central innovation is the **Skills + Code Execution** pattern, which replaces direct MCP tool loading with lightweight instruction files that delegate work to external scripts.

The term **"Reusable Intelligence"** refers to the packaging of domain expertise into self-contained skill units that any AI coding agent can consume. Each skill is a directory containing:

1. A `SKILL.md` file (~100 tokens) that tells the agent WHAT to do.
2. A `scripts/` directory with executable files that do the actual work (consumed at 0 context tokens).
3. Optional `references/` and `templates/` directories for on-demand documentation.

The **Cloud-Native** dimension provides skills for deploying applications on Kubernetes with Helm, Kafka, PostgreSQL, Dapr, and related infrastructure.

**Demo Application:** [LearnFlow](https://github.com/assadsharif/learnflow-app) -- an AI-powered Python tutoring platform built entirely using skills from this library.

---

## The Skills + Code Execution Pattern

The core architectural pattern that achieves **95%+ context token savings** compared to loading MCP tool definitions directly into the agent's context window.

```
Traditional Approach:
  Load 22 MCP servers directly --> ~50,000 context tokens consumed per session

Skills + Code Execution Pattern:
  SKILL.md (~100 tokens)  -->  scripts/*.py (executed externally, 0 tokens)  -->  minimal result returned
```

### How It Works

1. The AI agent reads `SKILL.md` -- a concise instruction file (~100 tokens) describing the skill's purpose, tool map, and execution commands.
2. The agent executes the script specified in the tool map (e.g., `python scripts/deploy.sh`). The script runs externally and consumes **zero context tokens** during execution.
3. Only the final result (exit code, summary output, file path) enters the agent's context window.

### Skill Directory Structure

```
.claude/skills/<skill-name>/
  SKILL.md           # Agent instructions (~100 tokens loaded into context)
  REFERENCE.md       # Detailed docs (loaded on-demand, not by default)
  scripts/
    deploy.sh        # Executed externally (0 context tokens)
    verify.py        # Executed externally (0 context tokens)
  templates/         # Optional scaffolding templates
  references/        # Optional reference documentation
```

### Two Skill Patterns

| Pattern | Description | Context Cost | Example |
|---------|-------------|-------------|---------|
| **MCP Code Execution** | SKILL.md + scripts/ -- agent executes scripts externally | ~100 tokens | `kafka-k8s-setup`, `agents-md-gen` |
| **Prompt-Only** | SKILL.md contains all guidance inline -- no scripts | ~200-500 tokens | `docker-containerization`, `interview` |

---

## Cross-Platform Compatibility

Skills are designed to work across multiple AI coding agents:

| Agent Platform | Format | How It Works |
|----------------|--------|-------------|
| **Claude Code** | `SKILL.md` + `scripts/` | Native support. Agent reads SKILL.md and executes scripts via bash/python. |
| **OpenAI Codex** | `SKILL.md` + `scripts/` | Same pattern. Codex reads SKILL.md instructions and runs scripts. |
| **Goose** | `recipe.yaml` | Equivalent format. Each skill can provide a `recipe.yaml` mapping to the same scripts. |

### Goose Recipe Example

```yaml
name: kafka-k8s-setup
description: Deploy Kafka on Kubernetes via Helm
steps:
  - run: bash .claude/skills/kafka-k8s-setup/scripts/deploy.sh
  - run: python .claude/skills/kafka-k8s-setup/scripts/verify.py
```

---

## Inventory Summary

| Metric | Count |
|--------|-------|
| Total Skills | 55 |
| Skills with Scripts (MCP Code Execution) | 24 |
| Prompt-Only Skills | 31 |
| Total Executable Scripts | 77 |
| Registered MCP Servers (.mcp.json) | 22 |
| Additional MCP Server Implementations | 6 |
| Total MCP Server Files | 28 |
| GitHub Actions Workflows | 2 |
| CI/CD Jobs | 6 |

---

## Skills Reference

### Cloud-Native & Kubernetes

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `k8s-foundation` | Check cluster health, apply Helm charts, verify K8s readiness | MCP Code Execution | `check_cluster.py`, `apply_chart.sh` |
| `kafka-k8s-setup` | Deploy Apache Kafka on K8s via Helm (Bitnami, Kraft mode) | MCP Code Execution | `deploy.sh`, `verify.py`, `create_topics.py` |
| `postgres-k8s-setup` | Deploy PostgreSQL on K8s via Helm, run migrations | MCP Code Execution | `deploy.sh`, `verify.py`, `migrate.py` |
| `nextjs-k8s-deploy` | Deploy Next.js apps on K8s with Docker + Helm | MCP Code Execution | `build_and_deploy.sh`, `verify.py` |
| `docusaurus-deploy` | Deploy Docusaurus documentation sites on K8s | MCP Code Execution | `init_docs.sh`, `deploy.sh`, `verify.py` |
| `kubernetes-deployment` | Generate K8s Deployment, Service, ConfigMap manifests from Pydantic schemas | Prompt-Only | -- |
| `helm-packaging` | Package applications into Helm charts for parameterized K8s deployments | Prompt-Only | -- |
| `minikube-cluster` | Manage local K8s cluster lifecycle, validate Helm readiness | Prompt-Only | -- |
| `kagent-analysis` | Analyze K8s cluster health, performance, and resource efficiency | Prompt-Only | -- |
| `kubectl-ai` | AI-assisted kubectl interface for K8s operations and diagnostics | Prompt-Only | -- |

### Backend & API Development

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `fastapi-backend` | FastAPI development with REST best practices, CRUD, Pydantic, middleware | MCP Code Execution | `init_fastapi.py`, `run_dev.sh` |
| `fastapi-dapr-agent` | Scaffold FastAPI + Dapr microservices with OpenAI Agents SDK | MCP Code Execution | `scaffold.py`, `init_dapr.sh` |
| `sqlmodel-orm` | SQLModel ORM guidance -- models, relationships, queries, FastAPI integration | MCP Code Execution | `init_models.py` |
| `neon-db` | Neon serverless PostgreSQL setup, connection pooling, branching | MCP Code Execution | `check_connection.py` |

### Frontend & UI

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `nextjs-app-router` | Next.js App Router (v13+), server/client components, data fetching | MCP Code Execution | `init_nextjs.sh` |
| `frontend-design` | Create distinctive, production-grade frontend interfaces | Prompt-Only | -- |
| `web-artifacts-builder` | Build multi-component claude.ai HTML artifacts (React, Tailwind, shadcn/ui) | MCP Code Execution | `init-artifact.sh`, `bundle-artifact.sh` |
| `theme-factory` | Apply professional font/color themes to artifacts (10 presets + custom) | Prompt-Only | -- |
| `vercel` | Manage Vercel deployments, projects, domains, environment variables | Prompt-Only | -- |

### AI & Agent Frameworks

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `openai-agents-sdk` | Build multi-agent workflows with tools, handoffs, guardrails (OpenAI Agents SDK) | Prompt-Only | -- |
| `openai-chatkit` | Build AI chat interfaces with ChatKit SDK (React, streaming, file uploads) | Prompt-Only | -- |
| `token-warden` | System-level token governor with budget limits and mode switching | Prompt-Only | -- |

### MCP Tooling & Protocol

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `mcp-code-execution` | Meta-pattern: convert MCP tool calls to Skills + Code Execution pattern | MCP Code Execution | `mcp_client.py`, `convert_mcp_to_skill.py` |
| `mcp-builder` | Guide for creating MCP servers (Python FastMCP / TypeScript MCP SDK) | MCP Code Execution | `connections.py`, `evaluation.py` |
| `mcp-sdk` | Build MCP servers/clients using official SDKs | Prompt-Only | -- |
| `fetch-mcp` | Web content fetching via Fetch MCP server | Prompt-Only | -- |
| `filesystem-mcp` | Secure filesystem operations via Filesystem MCP server | Prompt-Only | -- |
| `git-mcp` | Git repository operations via Git MCP server | Prompt-Only | -- |
| `github-mcp` | GitHub operations (repos, issues, PRs, workflows) via GitHub MCP server | Prompt-Only | -- |
| `memory-mcp` | Persistent semantic memory via Memory MCP server | Prompt-Only | -- |

### Testing & Quality

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `pytest-tdd` | Strict TDD with pytest -- Red-Green-Refactor, fixtures, parametrize, hypothesis | MCP Code Execution | `init_pytest.py`, `run_tdd_cycle.sh` |
| `TDD-Skill` | Test-Driven Development guidance and enforcement | Prompt-Only | -- |
| `webapp-testing` | Test local web applications using Playwright (screenshots, logs, UI verification) | MCP Code Execution | `with_server.py` |
| `zero-defect-debugger` | Strict diagnostic enforcer -- zero-tolerance error detection and blocking | Prompt-Only | -- |

### DevOps & CI/CD

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `docker-containerization` | AI-assisted containerization with Docker and Docker AI Agent (Gordon) | Prompt-Only | -- |
| `cicd-error-solver` | Diagnose and fix CI/CD pipeline failures (lint, build, test, workflow) | MCP Code Execution | `diagnose.py`, `fix_lint.sh`, `verify_ci.sh` |

### Document & Media Processing

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `pdf` | PDF manipulation -- extract text/tables, create, merge/split, fill forms, OCR | MCP Code Execution | 8 scripts (bounding boxes, form fields, fill, convert, validate) |
| `pptx` | PowerPoint creation, editing, analysis -- slides, layouts, thumbnails | MCP Code Execution | `html2pptx.js`, `inventory.py`, `rearrange.py`, `replace.py`, `thumbnail.py` |

### Skill Lifecycle (Meta)

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `skill-creator` | Guide for creating new Claude Code skills | MCP Code Execution | `init_skill.py`, `package_skill.py`, `quick_validate.py` |
| `skill-creator-pro` | Production-grade skill creation with context gathering from codebase | MCP Code Execution | `init_skill.py`, `package_skill.py`, `quick_validate.py` |
| `skill-validator` | Validate skills against production-level quality criteria | Prompt-Only | -- |
| `agents-md-gen` | Generate AGENTS.md manifests by scanning repository structure | MCP Code Execution | `generate_agents_md.py` |
| `interview` | Discovery conversations to understand user intent before taking action | Prompt-Only | -- |

### FTE Orchestration Suite

Full-Time-Equivalent autonomous agent orchestration skills:

| Skill | Purpose | Pattern |
|-------|---------|---------|
| `fte-vault-init` | Initialize Obsidian vault with canonical FTE folder layout | Prompt-Only |
| `fte-vault-status` | Display live task counts, pending approvals, vault health | Prompt-Only |
| `fte-vault-validate` | Run full validation suite (structure, state transitions, filenames) | Prompt-Only |
| `fte-task-triage` | Read inbox tasks, classify by priority/source, move to Needs_Action | Prompt-Only |
| `fte-approval-review` | Find pending approvals, present for decision, execute approve/reject | Prompt-Only |
| `fte-briefing-generate` | Generate CEO briefing from completed tasks, metrics, alerts | Prompt-Only |
| `fte-health-check` | Full system health check -- vault, watchers, orchestrator, security | Prompt-Only |
| `fte-orchestrator-status` | Show orchestrator liveness, queue depth, task throughput | Prompt-Only |
| `fte-security-scan` | Secrets and sensitive-data scan across the vault | Prompt-Only |
| `fte-watcher-status` | Display health/activity of registered watchers (Gmail, WhatsApp, etc.) | Prompt-Only |

### Utility & Infrastructure

| Skill | Purpose | Pattern | Scripts |
|-------|---------|---------|---------|
| `browsing-with-playwright` | Browser automation via Playwright MCP -- navigate, fill forms, scrape, screenshot | MCP Code Execution | `mcp-client.py`, `start-server.sh`, `stop-server.sh`, `verify.py` |
| `fetch-library-docs` | Fetch official library documentation with 60-90% token savings | MCP Code Execution | 18 scripts (fetch, extract, filter by type) |

---

## MCP Servers

### Registered Servers (22)

These servers are configured in `.mcp.json` and available for agent tool calls. All run as Python processes from `src/mcp_servers/`.

| # | Server Name | Script | Domain |
|---|-------------|--------|--------|
| 1 | `tdd_mcp` | `tdd_mcp.py` | Test-Driven Development lifecycle |
| 2 | `docker_containerization_mcp` | `docker_containerization_mcp.py` | Dockerfile generation, build commands, validation |
| 3 | `fastapi_backend_mcp` | `fastapi_backend_mcp.py` | FastAPI endpoint, model, schema generation |
| 4 | `web_content_fetch_mcp` | `web_content_fetch_mcp.py` | URL fetching (HTML, JSON, text, headers, links) |
| 5 | `sqlmodel_orm_mcp` | `sqlmodel_orm_mcp.py` | SQLModel table, schema, CRUD, query generation |
| 6 | `nextjs_app_router_mcp` | `nextjs_app_router_mcp.py` | Next.js page, layout, server action generation |
| 7 | `helm_packaging_mcp` | `helm_packaging_mcp.py` | Helm chart, values, helpers, deployment generation |
| 8 | `kubectl_ai_mcp` | `kubectl_ai_mcp.py` | kubectl prompt generation, pod/service/deployment diagnosis |
| 9 | `minikube_cluster_mcp` | `minikube_cluster_mcp.py` | Minikube config, addons, readiness, diagnostics |
| 10 | `kagent_analysis_mcp` | `kagent_analysis_mcp.py` | K8s cluster health, resource analysis, anti-pattern detection |
| 11 | `neon_db_mcp` | `neon_db_mcp.py` | Neon DB config, connection strings, pool config |
| 12 | `token_warden_mcp` | `token_warden_mcp.py` | Token budget enforcement, mode switching, audit |
| 13 | `openai_agents_mcp` | `openai_agents_mcp.py` | Agent, tool, handoff, guardrail, runner generation |
| 14 | `openai_chatkit_mcp` | `openai_chatkit_mcp.py` | Chat provider, hook, window, custom UI generation |
| 15 | `pdf_mcp` | `pdf_mcp.py` | PDF extraction, creation, merge/split, form, OCR code generation |
| 16 | `pptx_mcp` | `pptx_mcp.py` | PPTX extraction, creation, slide HTML, template code |
| 17 | `frontend_design_mcp` | `frontend_design_mcp.py` | Component, layout, typography, color, animation generation |
| 18 | `theme_factory_mcp` | `theme_factory_mcp.py` | Theme listing, CSS/Tailwind/Sass generation, contrast validation |
| 19 | `webapp_testing_mcp` | `webapp_testing_mcp.py` | Playwright test scripts, form tests, navigation, assertions |
| 20 | `web_artifacts_mcp` | `web_artifacts_mcp.py` | React component, page, layout, state, form generation |
| 21 | `interview_mcp` | `interview_mcp.py` | Request analysis, assumption surfacing, option generation |
| 22 | `quality_enforcer_mcp` | `quality_enforcer_mcp.py` | Diagnostic runs, error classification, clean validation |
| -- | `k8s_deployment_mcp` | `k8s_deployment_mcp.py` | K8s Deployment, Service, ConfigMap manifest generation |

### Additional Server Implementations (6)

These MCP server files exist in `src/mcp_servers/` but are not registered in `.mcp.json`. They are available for future activation or project-specific use.

| Server | Script | Domain |
|--------|--------|--------|
| `linkedin_mcp` | `linkedin_mcp.py` | LinkedIn social media integration |
| `meta_social_mcp` | `meta_social_mcp.py` | Meta (Facebook/Instagram) social integration |
| `twitter_mcp` | `twitter_mcp.py` | Twitter/X social media integration |
| `xero_accounting_mcp` | `xero_accounting_mcp.py` | Xero accounting/bookkeeping integration |

---

## CI/CD Pipeline

Two GitHub Actions workflows run on push/PR to `master`, `main`, and `develop` branches.

### Workflow 1: CI/CD Pipeline (`.github/workflows/ci.yml`)

| Job | Purpose | Details |
|-----|---------|---------|
| **lint** | Code formatting and linting | Black (formatting check) + Ruff (linting) on `src/` |
| **test** | Unit tests | pytest on Python 3.11 and 3.12 with pip caching |
| **validate-skills** | Skill structure validation | Verify every skill has `SKILL.md` and it is under 500 lines |
| **validate-scripts** | Script syntax checking | `py_compile` for all `.py` scripts, `bash -n` for all `.sh` scripts |
| **docs** | Documentation check | Verify `README.md` exists |
| **notify** | Aggregated status | Reports overall pass/fail across all jobs |

### Workflow 2: Detect Secrets (`.github/workflows/detect-secrets.yml`)

| Job | Purpose | Details |
|-----|---------|---------|
| **secret-scan** | Secrets detection | `detect-secrets` scan against baseline, PR-scoped scanning, auto-baseline updates on master |

---

## Directory Structure

```
.
+-- AGENTS.md                    # This file -- comprehensive agent manifest
+-- CLAUDE.md                    # Project-level agent instructions (SDD workflow)
+-- README.md                    # Project overview and quick start
+-- pyproject.toml               # Python package configuration (Python 3.11+)
+-- pytest.ini                   # Pytest configuration
|
+-- .claude/
|   +-- skills/                  # 55 reusable AI agent skills
|   |   +-- <skill-name>/
|   |   |   +-- SKILL.md         # Agent instructions (~100 tokens)
|   |   |   +-- REFERENCE.md     # Detailed documentation (on-demand)
|   |   |   +-- scripts/         # Executable scripts (0 context tokens)
|   |   |   +-- references/      # Additional reference material
|   |   |   +-- templates/       # Scaffolding templates
|   |   +-- ...
|   +-- agents/                  # Subagent configurations
|   +-- mcp/                     # MCP server configs
|
+-- src/
|   +-- mcp_servers/             # 28 MCP server implementations
|   |   +-- tdd_mcp.py
|   |   +-- fastapi_backend_mcp.py
|   |   +-- ...
|
+-- .mcp.json                    # MCP server registry (22 active servers)
|
+-- .specify/
|   +-- memory/
|   |   +-- constitution.md      # Project constitution (v1.0.0)
|   +-- templates/               # SDD templates (PHR, ADR, specs)
|
+-- specs/                       # Feature specifications (SDD)
+-- history/
|   +-- prompts/                 # Prompt History Records (PHR)
|   +-- adr/                     # Architecture Decision Records
+-- docs/                        # Project documentation
+-- tests/                       # Test suite
|
+-- .github/
    +-- workflows/
        +-- ci.yml               # CI/CD pipeline (lint, test, validate)
        +-- detect-secrets.yml   # Secret scanning workflow
```

---

## Constitution & Governance

The project follows **Spec-Driven Development (SDD)** with a ratified constitution at `.specify/memory/constitution.md` (v1.0.0, ratified 2026-02-11).

### Core Principles

| # | Principle | Summary |
|---|-----------|---------|
| I | Reusable Intelligence First | Every component designed for reuse across projects. No single-use code. |
| II | Cloud-Native by Default | Containerizable (Docker), orchestratable (K8s/Helm), twelve-factor app. |
| III | Spec-Driven Development | No code without a spec. Constitution > Specify > Plan > Tasks hierarchy. |
| IV | Test-First Quality Gate | TDD mandatory. Red-Green-Refactor. 80% minimum coverage. |
| V | MCP-First Tooling | MCP servers are first-class citizens. SHA256 verification. Rate limiting. |
| VI | Security & Secrets | Never hardcode secrets. OS keyring or vault in production. HITL for high-risk. |
| VII | Observability & Auditability | Structured JSON logging. All state changes logged. Health check endpoints. |
| VIII | Simplicity | YAGNI. Smallest viable diff. No unrelated refactoring. |

### Technology Stack

- **Language**: Python 3.11+ (primary), TypeScript/Node.js (frontend)
- **Backend**: FastAPI + SQLModel + Neon PostgreSQL
- **Frontend**: Next.js (App Router v13+) + Tailwind CSS
- **Containerization**: Docker (multi-stage builds)
- **Orchestration**: Kubernetes + Helm + Minikube (local)
- **Messaging**: Apache Kafka (Kraft mode)
- **Service Mesh**: Dapr (pub/sub + state management)
- **AI**: OpenAI Agents SDK + MCP servers
- **CI/CD**: GitHub Actions
- **Testing**: pytest + pytest-cov + hypothesis
