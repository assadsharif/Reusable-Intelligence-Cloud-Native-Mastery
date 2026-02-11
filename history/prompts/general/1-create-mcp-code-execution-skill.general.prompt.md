---
id: 1
title: Create MCP Code Execution Skill
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: user
command: create skill
labels: ["mcp", "skill", "code-execution", "meta-pattern", "scripts"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - .claude/skills/mcp-code-execution/SKILL.md
  - .claude/skills/mcp-code-execution/REFERENCE.md
  - .claude/skills/mcp-code-execution/scripts/mcp_client.py
  - .claude/skills/mcp-code-execution/scripts/convert_mcp_to_skill.py
tests:
  - none
---

## Prompt

Create the mcp-code-execution skill at this path: /mnt/c/Users/HomePC/Desktop/CODE/Hackathon III_ Reusable Intelligence and Cloud-Native Mastery/.claude/skills/mcp-code-execution/

This is the META-SKILL — it teaches how to wrap MCP server calls in executable scripts (the core pattern of the project).

Create these files:

1. SKILL.md — Purpose: The meta-pattern skill that wraps MCP server tool calls in executable scripts for zero-context-token execution. This skill explains AND automates the conversion of MCP tools into the Skills + Code Execution pattern.

Include:
- Frontmatter with name: mcp-code-execution, description about wrapping MCP tools in scripts
- Scope (Does: convert MCP tool definitions to executable scripts, create SKILL.md files, generate Goose recipes / Does NOT: run MCP servers, create new MCP tools)
- The Pattern section explaining: SKILL.md (~100 tokens) → scripts/*.py (executed, 0 tokens) → minimal result
- Why This Matters: Direct MCP loading bloats context with tool definitions (50k+ tokens for 22 servers). Scripts execute externally.
- Tool Map: mcp_client.py (call an MCP tool via CLI), convert_mcp_to_skill.py (generate a skill from an MCP server)
- Execution Pattern section
- Clarification Triggers (MCP server name, tool name, output format)
- Must Follow / Must Avoid
- Cross-Platform Compatibility with Goose recipe
- REFERENCE.md section explaining MCP protocol basics

2. REFERENCE.md — Detailed reference explaining:
- MCP Code Execution pattern in detail
- How to structure SKILL.md files
- How to write scripts that call MCP tools
- Token savings comparison table (direct load vs script execution)
- Example: converting kubernetes-deployment MCP to a skill

3. scripts/mcp_client.py — Python script that:
- Takes --server (MCP server name), --tool (tool name), --args (JSON string of args)
- Reads .mcp.json to find server config
- Spawns the MCP server process, sends a tool call via stdin/stdout JSON-RPC
- Returns the tool result as JSON
- Uses subprocess, no external MCP dependencies needed

4. scripts/convert_mcp_to_skill.py — Python script that:
- Takes --server-name, --output-dir, --description args
- Reads .mcp.json to find the server
- Generates a SKILL.md template with the correct tool map
- Creates a scripts/ directory with a wrapper script for each tool
- Creates a recipe.yaml for Goose compatibility
- Prints summary of generated files

Make sure all scripts have shebangs and use argparse.

## Response snapshot

Created the complete mcp-code-execution skill with 4 files:
- SKILL.md: Meta-pattern skill with frontmatter, scope, pattern explanation, token savings table, tool map, execution patterns, clarification triggers, must-follow/must-avoid, cross-platform compatibility section, and REFERENCE.md pointer.
- REFERENCE.md: Detailed reference with MCP protocol basics, SKILL.md structure guide, script writing patterns (wrapper and direct JSON-RPC), token savings analysis (91-97% savings vs direct load), and full worked example converting k8s_deployment_mcp.
- scripts/mcp_client.py: Standalone MCP client using subprocess stdio JSON-RPC. Auto-discovers .mcp.json, spawns server, handles initialize handshake, supports --list-tools and --tool calls, returns JSON. Uses argparse, threading, queue — no external deps.
- scripts/convert_mcp_to_skill.py: Skill generator that discovers tools via tools/list, generates SKILL.md with tool map, creates per-tool wrapper scripts with argparse, copies mcp_client.py, generates recipe.yaml for Goose.

## Outcome

- Impact: Core meta-skill created; enables converting any of 22 MCP servers to the Skills + Code Execution pattern
- Tests: none (scripts use subprocess/stdio, manual verification needed)
- Files: 4 files created in .claude/skills/mcp-code-execution/
- Next prompts: Test mcp_client.py against a live MCP server, run convert_mcp_to_skill.py to generate a skill, validate generated output
- Reflection: Followed existing skill conventions from browsing-with-playwright and kubernetes-deployment skills; mcp_client.py modeled after the universal client pattern already in the project

## Evaluation notes (flywheel)

- Failure modes observed: None yet; untested against live servers
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Run mcp_client.py --server docker_containerization_mcp --list-tools to verify stdio handshake works
