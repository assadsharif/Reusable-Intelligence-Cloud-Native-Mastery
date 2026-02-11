# Reusable Intelligence & Cloud-Native Mastery Constitution

## Core Principles

### I. Reusable Intelligence First
Every component MUST be designed for reuse across projects and contexts. Skills, MCP servers, agents, and libraries are self-contained units with clear interfaces. No single-use throwaway code — if it solves a problem once, package it to solve it everywhere.

### II. Cloud-Native by Default
All services MUST be containerizable (Docker), orchestratable (Kubernetes/Helm), and deployable to any cloud provider. Twelve-factor app principles apply. Configuration via environment variables, stateless processes, disposable containers.

### III. Spec-Driven Development (NON-NEGOTIABLE)
No code without a spec. The SDD lifecycle is mandatory:
- **Constitution** (WHY) → **Specify** (WHAT) → **Plan** (HOW) → **Tasks** (BREAKDOWN) → **Implement** (CODE)
- Every code change MUST reference a Task ID
- The hierarchy `Constitution > Specify > Plan > Tasks` resolves all conflicts

### IV. Test-First Quality Gate
TDD is mandatory for all production code:
- Tests written and approved BEFORE implementation
- Red-Green-Refactor cycle strictly enforced
- Integration tests required for: API contracts, cross-service communication, data schemas
- Minimum 80% code coverage for new features

### V. MCP-First Tooling
MCP (Model Context Protocol) servers are first-class citizens:
- Every reusable capability SHOULD be exposed as an MCP tool
- MCP servers MUST be verified (SHA256 checksums) before execution
- Rate limiting and circuit breakers MUST protect all MCP endpoints
- Skills and agents MUST prefer MCP tools over shell commands for discovery and execution

### VI. Security & Secrets Management
- NEVER hardcode secrets, tokens, or credentials in source code
- Use `.env` files for local development, environment variables for production
- Secrets MUST use OS keyring or vault-based storage in production
- All security events MUST be logged to an append-only audit trail
- HITL (Human-in-the-Loop) approval required for high-risk operations

### VII. Observability & Auditability
- Structured logging (JSON) required for all services
- All state changes MUST be logged with: timestamp, action, actor, result, approval status
- Metrics collection (throughput, latency, error rate) for all services
- Health check endpoints required for every deployed service

### VIII. Simplicity & Smallest Viable Change
- YAGNI: Do not build for hypothetical future requirements
- Prefer the smallest diff that satisfies the spec
- Do not refactor unrelated code in a feature branch
- Start simple, iterate based on measured need

## Technology Stack

### Required
- **Language**: Python 3.11+ (primary), TypeScript/Node.js (frontend/tooling)
- **API Framework**: FastAPI (REST APIs)
- **ORM**: SQLModel (database models)
- **Database**: Neon PostgreSQL (serverless, production), SQLite (local dev)
- **Containerization**: Docker with multi-stage builds
- **Orchestration**: Kubernetes + Helm charts
- **CI/CD**: GitHub Actions
- **Testing**: pytest + pytest-cov + hypothesis

### Preferred
- **Frontend**: Next.js (App Router, v13+)
- **Styling**: Tailwind CSS
- **AI Integration**: OpenAI Agents SDK, MCP servers
- **Local K8s**: Minikube for development
- **Monitoring**: Structured logs + health checks (Prometheus/Grafana optional)

## Development Workflow

### Branch Strategy
- `main` — production-ready, protected
- `feature/<spec-number>-<name>` — feature branches from spec
- All merges via Pull Request with review

### Quality Gates (MUST pass before merge)
1. All tests pass (`pytest --strict-markers`)
2. No secrets detected (`detect-secrets scan`)
3. Code references Task IDs in comments
4. PR description links to spec and tasks
5. Constitution compliance verified

### Code Standards
- Type hints required for all public functions
- Docstrings required for all public classes and functions
- Black formatting (line length 88)
- isort for import ordering
- No `# type: ignore` without justification comment

## Governance

This constitution supersedes all other project practices. Amendments require:
1. Explicit discussion and approval
2. Updated version number and date
3. Migration plan for any breaking changes to existing code

All PRs and reviews MUST verify constitutional compliance. Complexity MUST be justified against Principle VIII (Simplicity).

**Version**: 1.0.0 | **Ratified**: 2026-02-11 | **Last Amended**: 2026-02-11
