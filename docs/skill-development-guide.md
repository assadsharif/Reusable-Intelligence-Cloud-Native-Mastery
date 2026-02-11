# Skill Development Guide

Guide to creating reusable AI agent skills with the MCP Code Execution pattern.

## Overview

The Skills + Code Execution pattern wraps AI agent capabilities in executable scripts that run externally (0 context tokens) instead of loading MCP tool definitions directly (~2,500 tokens each).

```
SKILL.md (~100 tokens) → scripts/*.py (executed, 0 tokens) → minimal result
```

## Skill Structure

```
.claude/skills/<skill-name>/
├── SKILL.md           # Required: Agent instructions
├── REFERENCE.md       # Optional: Detailed documentation
├── scripts/
│   ├── main_action.sh # Required: Executable scripts
│   └── verify.py
└── templates/         # Optional: File templates
```

## Creating a New Skill

### Step 1: Define the SKILL.md

The SKILL.md is the only file loaded into the agent's context. Keep it lean (~100 tokens).

Required sections:

```markdown
---
name: my-skill
description: |
  One-line description. Triggers on: "keyword1", "keyword2".
---

# Skill Name

Brief description of what this skill does.

## Scope
**Does**: What capabilities this skill provides
**Does NOT**: What it explicitly excludes

## Tool Map
| Action | Script | Input | Output |
|--------|--------|-------|--------|
| Deploy | scripts/deploy.sh | --namespace | Status JSON |
| Verify | scripts/verify.py | --namespace | Health report |

## Clarification Triggers
### Required
1. **Action** — which operation to perform?

### Optional
2. **Namespace** — target K8s namespace (default: `default`)

## Must Follow
- Always verify prerequisites before executing
- Output structured JSON for machine parsing
- Use resource-constrained settings for Minikube

## Must Avoid
- Hardcoding credentials
- Skipping verification steps
```

### Step 2: Write the Scripts

Scripts do the actual work. They should:
- Accept arguments via CLI flags (argparse for Python, getopts for bash)
- Output structured JSON when possible
- Exit with non-zero code on failure
- Include usage comments at the top

**Python script template:**
```python
#!/usr/bin/env python3
"""Brief description.

Usage:
    python script.py --flag value
"""
import argparse
import json
import subprocess
import sys

def run_cmd(cmd: list[str], timeout: int = 60) -> tuple[int, str, str]:
    try:
        r = subprocess.run(cmd, capture_output=True, text=True, timeout=timeout)
        return r.returncode, r.stdout, r.stderr
    except (subprocess.TimeoutExpired, FileNotFoundError) as e:
        return 1, "", str(e)

def main():
    parser = argparse.ArgumentParser(description="Script description")
    parser.add_argument("--namespace", "-n", default="default")
    args = parser.parse_args()

    # Do work
    result = {"status": "ok", "namespace": args.namespace}
    print(json.dumps(result, indent=2))

if __name__ == "__main__":
    main()
```

**Bash script template:**
```bash
#!/usr/bin/env bash
# Brief description.
# Usage: bash script.sh --namespace my-ns
set -euo pipefail

NAMESPACE="default"
while [[ $# -gt 0 ]]; do
    case "$1" in
        --namespace|-n) NAMESPACE="$2"; shift 2 ;;
        *) echo "Unknown: $1"; exit 1 ;;
    esac
done

echo "Working in namespace: $NAMESPACE"
# Do work here
```

### Step 3: Add Cross-Platform Support

For Goose compatibility, add a recipe.yaml section to SKILL.md:

```yaml
# Goose recipe.yaml
name: my-skill
description: What this skill does
steps:
  - run: bash .claude/skills/my-skill/scripts/deploy.sh
  - run: python .claude/skills/my-skill/scripts/verify.py
```

### Step 4: Test the Skill

1. Load the skill in Claude Code (it auto-detects from `.claude/skills/`)
2. Give a single prompt matching the trigger keywords
3. Verify the agent reads SKILL.md, executes scripts, and returns the result

## Best Practices

1. **Keep SKILL.md lean** — Under 100 tokens of instructions
2. **Structured output** — Scripts output JSON for easy parsing
3. **Tool Map** — Always include the action-to-script mapping table
4. **Guardrails** — Must Follow / Must Avoid sections prevent common mistakes
5. **Clarification Triggers** — Tell the agent what to ask when information is missing
6. **Verification** — Always include a verify script to check results
7. **Cross-platform** — Include Goose recipe.yaml for portability

## Token Savings Analysis

| Approach | Per Tool | 22 MCP Servers | Savings |
|----------|---------|---------------|---------|
| Direct MCP Load | ~2,500 tokens | ~50,000 tokens | — |
| Skills + Code Execution | ~100 tokens | ~2,200 tokens | **95.6%** |

## Examples

See these skills for reference implementations:
- `kafka-k8s-setup` — Infrastructure deployment skill
- `fastapi-dapr-agent` — Service scaffolding skill
- `mcp-code-execution` — Meta-pattern skill (converts MCP tools to skills)
- `agents-md-gen` — Repository analysis skill
