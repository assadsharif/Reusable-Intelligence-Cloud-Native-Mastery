# Reusable Intelligence & Cloud-Native Mastery

> **Hackathon III** — Portable AI agent skills with the MCP Code Execution pattern, deployed on cloud-native infrastructure.

## The Core Innovation

**Skills + Code Execution** replaces direct MCP tool loading with executable scripts, achieving **95%+ context token savings**:

```
Traditional:  Load 22 MCP servers → ~50,000 context tokens consumed
Our Pattern:  SKILL.md (~100 tokens) → scripts/*.py (0 tokens) → minimal result
```

Each Skill is a self-contained package:
```
.claude/skills/<name>/
├── SKILL.md           # Agent instructions (~100 tokens)
├── REFERENCE.md       # Detailed docs (on-demand)
├── scripts/
│   ├── deploy.sh      # Executed externally (0 context tokens)
│   └── verify.py
└── templates/         # Optional
```

## Hackathon Skills (8 New)

| Skill | Purpose | Scripts | Pattern |
|-------|---------|---------|---------|
| `agents-md-gen` | Generate AGENTS.md manifests | 1 | MCP Code Execution |
| `k8s-foundation` | Cluster health + Helm charts | 2 | MCP Code Execution |
| `kafka-k8s-setup` | Deploy Kafka on K8s (Kraft) | 3 | MCP Code Execution |
| `postgres-k8s-setup` | Deploy PostgreSQL on K8s | 3 | MCP Code Execution |
| `fastapi-dapr-agent` | Scaffold FastAPI + Dapr + Agents | 2 | MCP Code Execution |
| `nextjs-k8s-deploy` | Deploy Next.js on K8s | 2 | MCP Code Execution |
| `mcp-code-execution` | Meta: convert MCP tools to skills | 2 | MCP Code Execution |
| `docusaurus-deploy` | Deploy docs sites on K8s | 3 | MCP Code Execution |

## Full Inventory

**54 skills** | **23 MCP servers** | **74 scripts**

See [AGENTS.md](AGENTS.md) for the complete inventory.

## Cross-Platform Portability

Skills work across multiple AI agents:

| Agent | Format | Status |
|-------|--------|--------|
| Claude Code | SKILL.md | Supported |
| OpenAI Codex | SKILL.md | Supported |
| Goose | recipe.yaml | Supported |

## Cloud-Native Stack

| Component | Technology |
|-----------|-----------|
| Orchestration | Kubernetes (Minikube local) |
| Packaging | Helm (Bitnami charts) |
| Messaging | Apache Kafka (Kraft mode) |
| Database | PostgreSQL |
| Service Mesh | Dapr (pub/sub + state) |
| Backend | FastAPI + OpenAI Agents SDK |
| Frontend | Next.js 14 + Monaco Editor |
| AI Context | MCP (Model Context Protocol) |

## Demo Application: LearnFlow

AI-powered Python tutoring platform built entirely using Skills from this library.

**Repository:** [assadsharif/learnflow-app](https://github.com/assadsharif/learnflow-app)

- 6 AI tutoring agents (Triage, Concepts, Code Review, Debug, Exercise, Progress)
- Multi-agent orchestration with OpenAI Agents SDK
- Dapr service mesh for Kafka pub/sub and PostgreSQL state
- Kubernetes deployment with Helm charts

## Quick Start

```bash
# Clone
git clone https://github.com/assadsharif/Reusable-Intelligence-Cloud-Native-Mastery.git
cd Reusable-Intelligence-Cloud-Native-Mastery

# Set up environment
python3 -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"

# Start Minikube
minikube start --cpus=4 --memory=4096 --driver=docker

# Use a skill (example: deploy Kafka)
bash .claude/skills/kafka-k8s-setup/scripts/deploy.sh

# Verify
python .claude/skills/kafka-k8s-setup/scripts/verify.py
```

## Project Structure

```
.claude/
├── skills/           # 54 reusable skills
│   ├── kafka-k8s-setup/
│   │   ├── SKILL.md
│   │   └── scripts/
│   ├── fastapi-dapr-agent/
│   └── ...
├── agents/           # Subagent configurations
└── mcp/              # MCP server configs

src/mcp_servers/      # 23 MCP server implementations
AGENTS.md             # Auto-generated skill inventory
CLAUDE.md             # Agent instructions
```

## License

MIT
