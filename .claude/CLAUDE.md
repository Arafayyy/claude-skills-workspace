# Claude Workspace Instructions

This file is the shared brain for this workspace.

It defines how Claude should behave across the local agents and skills stored in `.claude/`.
More specific instructions inside an agent or skill may override this file when needed.

## Purpose

This repository is a workspace for building and maintaining:

- shared Claude instructions
- focused subagents
- reusable skills
- helper scripts that support those skills

The goal is to keep the system simple, practical, and easy to extend.

## Current Workspace Structure

- `.claude/CLAUDE.md` - Shared global instructions
- `.claude/agents/` - Focused agents for narrow tasks
- `.claude/skills/` - Skills made of `SKILL.md` files and optional `scripts/`
- `.claude/rules/` - Additional local Claude rules
- `.tmp/` - Temporary generated outputs when needed

## Current Skills

- `add-webhook` - Guidance for creating new Modal webhook directives and wiring them into a larger webhook system
- `design-website` - Reads prospect data and generates a premium one-page HTML mockup

## Current Subagents

- `code-reviewer` - Reviews code and reports issues by severity
- `email-classifier` - Classifies Gmail-style email tasks
- `qa` - Helps generate and run tests
- `research` - Gathers focused research and context
- `tell-me-the-time` - Answers time and date questions using the live system clock

## Default Behavior

- Read the local workspace before making assumptions.
- Prefer current files over memory.
- Make the smallest useful change that fully solves the problem.
- Keep instructions, scripts, and documentation aligned.
- If something in the workspace looks like a template, prefer the files that actually exist.

## How To Work With Skills

- Every skill lives in its own folder inside `.claude/skills/`.
- The main entrypoint for a skill is `SKILL.md`.
- If a skill has automation, keep it in that skill's `scripts/` directory.
- If a skill needs human-facing setup or usage notes, add a local `README.md`.
- Update the skill documentation when you learn something important about its workflow.

## How To Work With Agents

- Every agent lives in `.claude/agents/` as a markdown file.
- Keep agents narrow and task-specific.
- Agent files should usually describe:
  - purpose
  - when to use the agent
  - behavior rules
  - commands or tools to prefer
  - output style
  - guardrails

## Local Conventions

- Prefer local verification over guessing.
- Prefer deterministic scripts for repeatable work.
- Keep generated artifacts out of version control when appropriate.
- Use `.tmp/` for disposable outputs when a skill generates files.
- Do not list tools, directories, or infrastructure that do not exist in this workspace.

## Setup Assumptions

This workspace does not assume a full production automation stack by default.
Only rely on tools or files that are actually present in the repo.

Known current assumptions:

- Python is needed for the `design-website` skill scripts
- Google OAuth credentials may be needed for Google Sheets access in `design-website`
- `UNSPLASH_ACCESS_KEY` may be used by `design-website` for stock images
- Some skills, like `add-webhook`, may describe external infrastructure that belongs to a larger system and is not fully present in this repo

## Editing Principles

- Preserve the existing structure unless there is a clear reason to improve it.
- Keep docs concise and easy to scan.
- Put reusable logic into scripts instead of bloating prompt files.
- Prefer direct examples over abstract explanations.
- When changing a skill, check whether its `README.md` or `SKILL.md` should also be updated.

## Accuracy Rules

- Do not claim a file, directory, dependency, or integration exists unless it is present or explicitly provided by the user.
- If setup details are missing, say so plainly.
- If a skill depends on external systems, describe that dependency clearly instead of implying it is already configured here.

## Summary

This workspace is the home for all local Claude skills and agents.
Keep it grounded in the actual repo, easy to extend, and consistent across docs, prompts, and scripts.
