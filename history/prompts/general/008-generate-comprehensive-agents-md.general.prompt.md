---
id: 008
title: Generate Comprehensive AGENTS.md
stage: general
date: 2026-02-12
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: asad
command: generate AGENTS.md
labels: ["agents-md", "documentation", "skills-inventory", "mcp-servers"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - AGENTS.md
tests:
  - none
---

## Prompt

Generate an AGENTS.md file for the skills-library repository at "/mnt/c/Users/HomePC/Desktop/CODE/Hackathon III_ Reusable Intelligence and Cloud-Native Mastery".

This repo is the "Reusable Intelligence & Cloud-Native Mastery" skills library. Scan the codebase to discover:
1. All skills in `.claude/skills/` (each has a SKILL.md and often scripts/)
2. All MCP servers in `src/mcp_servers/`
3. The .mcp.json config
4. GitHub Actions workflows in `.github/workflows/`
5. The CLAUDE.md project instructions
6. Key project files (README.md, pyproject.toml, constitution)

Then create a comprehensive AGENTS.md at the repo root with:
- Project overview (Reusable Intelligence = portable AI agent skills with MCP Code Execution pattern)
- GitHub: github.com/assadsharif/Reusable-Intelligence-Cloud-Native-Mastery
- Agent configurations section listing all skills with their purpose
- MCP servers section listing all 22 servers
- CI/CD pipeline overview
- The Skills + Code Execution pattern explanation (SKILL.md ~100 tokens -> scripts/*.py executed at 0 tokens -> minimal result)
- Cross-platform compatibility (Claude Code, OpenAI Codex, Goose)
- Key directory structure

Write the AGENTS.md file to the repo root. Make it comprehensive but well-organized.

## Response snapshot

Generated a comprehensive AGENTS.md (395 lines) at the repository root. Scanned all 55 SKILL.md files across `.claude/skills/`, all 28 MCP server implementations in `src/mcp_servers/`, both CI/CD workflows, the constitution, README.md, pyproject.toml, and .mcp.json. The file includes: Table of Contents, Project Overview, Skills + Code Execution Pattern explanation, Cross-Platform Compatibility section, Inventory Summary (55 skills, 28 MCP servers, 77 scripts), categorized Skills Reference (11 categories), MCP Servers listing (22 registered + 6 additional), CI/CD Pipeline overview, Directory Structure, and Constitution & Governance.

## Outcome

- Impact: Generated comprehensive agent manifest documenting the full skills library inventory
- Tests: none
- Files: 1 file written (AGENTS.md)
- Next prompts: Commit the AGENTS.md, validate with skill-validator, update README skill counts if needed
- Reflection: Thorough scan of all 55 skill directories and 28 MCP server files provided accurate categorization. Counted 77 scripts across the codebase and identified 6 MCP servers not in .mcp.json.

## Evaluation notes (flywheel)

- Failure modes observed: None
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): N/A
