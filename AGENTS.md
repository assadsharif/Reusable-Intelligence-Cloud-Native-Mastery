# AGENTS.md

> Auto-generated on 2026-02-11 by agents-md-gen skill

## Summary

| Metric | Count |
|--------|-------|
| Skills | 54 |
| Skills with Scripts (MCP Code Execution) | 23 |
| Total Scripts | 74 |
| MCP Servers | 23 |
| Goose Compatible | No |

## Project Agent Instructions

This file is generated during init for the selected agent.

## Skills Inventory

| Skill | Scripts | References | Pattern | Path |
|-------|---------|------------|---------|------|
| TDD-Skill | - | Yes | Prompt-only | `.claude/skills/TDD-Skill` |
| agents-md-gen | 1 scripts | - | MCP Code Execution | `.claude/skills/agents-md-gen` |
| browsing-with-playwright | 4 scripts | Yes | MCP Code Execution | `.claude/skills/browsing-with-playwright` |
| docker-containerization | - | Yes | Prompt-only | `.claude/skills/docker-containerization` |
| docusaurus-deploy | 3 scripts | - | MCP Code Execution | `.claude/skills/docusaurus-deploy` |
| fastapi-backend | 2 scripts | Yes | MCP Code Execution | `.claude/skills/fastapi-backend` |
| fastapi-dapr-agent | 2 scripts | - | MCP Code Execution | `.claude/skills/fastapi-dapr-agent` |
| fetch-library-docs | 18 scripts | Yes | MCP Code Execution | `.claude/skills/fetch-library-docs` |
| fetch-mcp | - | Yes | Prompt-only | `.claude/skills/fetch-mcp` |
| filesystem-mcp | - | Yes | Prompt-only | `.claude/skills/filesystem-mcp` |
| frontend-design | - | - | Prompt-only | `.claude/skills/frontend-design` |
| fte-approval-review | - | - | Prompt-only | `.claude/skills/fte-approval-review` |
| fte-briefing-generate | - | - | Prompt-only | `.claude/skills/fte-briefing-generate` |
| fte-health-check | - | - | Prompt-only | `.claude/skills/fte-health-check` |
| fte-orchestrator-status | - | - | Prompt-only | `.claude/skills/fte-orchestrator-status` |
| fte-security-scan | - | - | Prompt-only | `.claude/skills/fte-security-scan` |
| fte-task-triage | - | - | Prompt-only | `.claude/skills/fte-task-triage` |
| fte-vault-init | - | - | Prompt-only | `.claude/skills/fte-vault-init` |
| fte-vault-status | - | - | Prompt-only | `.claude/skills/fte-vault-status` |
| fte-vault-validate | - | - | Prompt-only | `.claude/skills/fte-vault-validate` |
| fte-watcher-status | - | - | Prompt-only | `.claude/skills/fte-watcher-status` |
| git-mcp | - | Yes | Prompt-only | `.claude/skills/git-mcp` |
| github-mcp | - | Yes | Prompt-only | `.claude/skills/github-mcp` |
| helm-packaging | - | Yes | Prompt-only | `.claude/skills/helm-packaging` |
| interview | - | Yes | Prompt-only | `.claude/skills/interview` |
| k8s-foundation | 2 scripts | - | MCP Code Execution | `.claude/skills/k8s-foundation` |
| kafka-k8s-setup | 3 scripts | - | MCP Code Execution | `.claude/skills/kafka-k8s-setup` |
| kagent-analysis | - | Yes | Prompt-only | `.claude/skills/kagent-analysis` |
| kubectl-ai | - | Yes | Prompt-only | `.claude/skills/kubectl-ai` |
| kubernetes-deployment | - | Yes | Prompt-only | `.claude/skills/kubernetes-deployment` |
| mcp-builder | 4 scripts | - | MCP Code Execution | `.claude/skills/mcp-builder` |
| mcp-code-execution | 2 scripts | Yes | MCP Code Execution | `.claude/skills/mcp-code-execution` |
| mcp-sdk | - | - | Prompt-only | `.claude/skills/mcp-sdk` |
| memory-mcp | - | Yes | Prompt-only | `.claude/skills/memory-mcp` |
| minikube-cluster | - | Yes | Prompt-only | `.claude/skills/minikube-cluster` |
| neon-db | 1 scripts | Yes | MCP Code Execution | `.claude/skills/neon-db` |
| nextjs-app-router | 1 scripts | Yes | MCP Code Execution | `.claude/skills/nextjs-app-router` |
| nextjs-k8s-deploy | 2 scripts | - | MCP Code Execution | `.claude/skills/nextjs-k8s-deploy` |
| openai-agents-sdk | - | - | Prompt-only | `.claude/skills/openai-agents-sdk` |
| openai-chatkit | - | - | Prompt-only | `.claude/skills/openai-chatkit` |
| pdf | 8 scripts | Yes | MCP Code Execution | `.claude/skills/pdf` |
| postgres-k8s-setup | 3 scripts | - | MCP Code Execution | `.claude/skills/postgres-k8s-setup` |
| pptx | 5 scripts | - | MCP Code Execution | `.claude/skills/pptx` |
| pytest-tdd | 2 scripts | Yes | MCP Code Execution | `.claude/skills/pytest-tdd` |
| skill-creator | 3 scripts | Yes | MCP Code Execution | `.claude/skills/skill-creator` |
| skill-creator-pro | 3 scripts | Yes | MCP Code Execution | `.claude/skills/skill-creator-pro` |
| skill-validator | - | Yes | Prompt-only | `.claude/skills/skill-validator` |
| sqlmodel-orm | 1 scripts | Yes | MCP Code Execution | `.claude/skills/sqlmodel-orm` |
| theme-factory | - | - | Prompt-only | `.claude/skills/theme-factory` |
| token-warden | - | - | Prompt-only | `.claude/skills/token-warden` |
| vercel | 0 scripts | Yes | MCP Code Execution | `.claude/skills/vercel` |
| web-artifacts-builder | 3 scripts | - | MCP Code Execution | `.claude/skills/web-artifacts-builder` |
| webapp-testing | 1 scripts | - | MCP Code Execution | `.claude/skills/webapp-testing` |
| zero-defect-debugger | - | Yes | Prompt-only | `.claude/skills/zero-defect-debugger` |

## MCP Servers

| Server | Script |
|--------|--------|
| docker_containerization_mcp | `docker_containerization_mcp.py` |
| fastapi_backend_mcp | `fastapi_backend_mcp.py` |
| frontend_design_mcp | `frontend_design_mcp.py` |
| helm_packaging_mcp | `helm_packaging_mcp.py` |
| interview_mcp | `interview_mcp.py` |
| k8s_deployment_mcp | `k8s_deployment_mcp.py` |
| kagent_analysis_mcp | `kagent_analysis_mcp.py` |
| kubectl_ai_mcp | `kubectl_ai_mcp.py` |
| minikube_cluster_mcp | `minikube_cluster_mcp.py` |
| neon_db_mcp | `neon_db_mcp.py` |
| nextjs_app_router_mcp | `nextjs_app_router_mcp.py` |
| openai_agents_mcp | `openai_agents_mcp.py` |
| openai_chatkit_mcp | `openai_chatkit_mcp.py` |
| pdf_mcp | `pdf_mcp.py` |
| pptx_mcp | `pptx_mcp.py` |
| quality_enforcer_mcp | `quality_enforcer_mcp.py` |
| sqlmodel_orm_mcp | `sqlmodel_orm_mcp.py` |
| tdd_mcp | `tdd_mcp.py` |
| theme_factory_mcp | `theme_factory_mcp.py` |
| token_warden_mcp | `token_warden_mcp.py` |
| web_artifacts_mcp | `web_artifacts_mcp.py` |
| web_content_fetch_mcp | `web_content_fetch_mcp.py` |
| webapp_testing_mcp | `webapp_testing_mcp.py` |

## Architecture: Skills + Code Execution Pattern

```
SKILL.md (~100 tokens) → scripts/*.py (executed, 0 tokens) → minimal result
```

Skills with the **MCP Code Execution** pattern keep the AI context window lean by executing scripts externally rather than loading MCP tool definitions directly.
