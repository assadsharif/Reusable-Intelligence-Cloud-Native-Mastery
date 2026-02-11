---
id: 005
title: Validate Four Skills Against Criteria
stage: general
date: 2026-02-11
surface: agent
model: claude-opus-4-6
feature: none
branch: master
user: asad
command: skill-validation
labels: ["skill-validation", "quality-assurance", "agents-md-gen", "k8s-foundation", "kafka-k8s-setup", "postgres-k8s-setup"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:
  - .claude/skills/agents-md-gen/SKILL.md
  - .claude/skills/agents-md-gen/scripts/generate_agents_md.py
  - .claude/skills/k8s-foundation/SKILL.md
  - .claude/skills/k8s-foundation/scripts/check_cluster.py
  - .claude/skills/k8s-foundation/scripts/apply_chart.sh
  - .claude/skills/kafka-k8s-setup/SKILL.md
  - .claude/skills/kafka-k8s-setup/scripts/deploy.sh
  - .claude/skills/kafka-k8s-setup/scripts/verify.py
  - .claude/skills/kafka-k8s-setup/scripts/create_topics.py
  - .claude/skills/postgres-k8s-setup/SKILL.md
  - .claude/skills/postgres-k8s-setup/scripts/deploy.sh
  - .claude/skills/postgres-k8s-setup/scripts/verify.py
  - .claude/skills/postgres-k8s-setup/scripts/migrate.py
tests:
  - none (read-only validation)
---

## Prompt

You are applying the skill-validator criteria to evaluate 4 skills. For each skill, read its SKILL.md and any scripts/references, then score it against the 7 criteria categories (Structure & Anatomy 15%, Content Quality 20%, User Interaction 15%, Documentation 15%, Domain Standards 15%, Technical Robustness 10%, Maintainability 10%). Each criterion scores 0-3. Output a validation report for each skill.

Skills to validate (read SKILL.md and all scripts for each):

1. `.claude/skills/agents-md-gen/SKILL.md` - Scripts: `scripts/generate_agents_md.py`
2. `.claude/skills/k8s-foundation/SKILL.md` - Scripts: `scripts/check_cluster.py`, `scripts/apply_chart.sh`
3. `.claude/skills/kafka-k8s-setup/SKILL.md` - Scripts: `scripts/deploy.sh`, `scripts/verify.py`, `scripts/create_topics.py`
4. `.claude/skills/postgres-k8s-setup/SKILL.md` - Scripts: `scripts/deploy.sh`, `scripts/verify.py`, `scripts/migrate.py`

For EACH skill, produce a report with Rating, Overall Score, Summary, Category Scores table, Critical Issues, Improvement Recommendations, and Strengths.

## Response snapshot

Produced detailed validation reports for all 4 skills:
- **agents-md-gen**: 88/100 (Production) - Clean single-purpose builder skill, well-implemented Python scanner
- **k8s-foundation**: 90/100 (Production) - Robust health checking with structured JSON output, strong Helm integration
- **kafka-k8s-setup**: 86/100 (Good) - Good lifecycle coverage with Kraft mode, needs broker readiness check before topic creation
- **postgres-k8s-setup**: 91/100 (Production) - Most complete skill; migration script with stop-on-failure, pod discovery, PVC verification

Common strengths: consistent SKILL.md structure, Skills + Code Execution pattern adherence, proper arg parsing, strict Bash mode.
Common gaps: no tests, duplicated run_cmd helper, no version fields, no retry logic.

## Outcome

- Impact: Quality assessment completed for 4 skills; identified specific improvement actions
- Tests: No tests run (read-only analysis)
- Files: 13 files read across 4 skills (4 SKILL.md + 9 scripts)
- Next prompts: Address high-priority recommendations (JSON error handling in agents-md-gen, dry-run in k8s-foundation, readiness check in kafka-k8s-setup, PGPASSWORD exposure in postgres-k8s-setup)
- Reflection: All skills follow the pattern well; the main differentiation is in error handling depth and operational completeness

## Evaluation notes (flywheel)

- Failure modes observed: None - all skills are structurally sound
- Graders run and results (PASS/FAIL): Manual review PASS for all skills at their respective rating levels
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): Add shared run_cmd utility and test scaffolding across all skills
