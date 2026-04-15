# Claude Workspace

This repository is a local workspace for building, organizing, and evolving Claude agents and skills.

It acts as a home base for:

- shared system instructions
- focused subagents
- reusable skills
- helper scripts and local conventions

## Structure

- [.claude/CLAUDE.md](/home/abdur-rafay/claude-code/.claude/CLAUDE.md) - Shared brain and default behavior for the workspace
- `.claude/agents/` - Task-specific agents with narrow responsibilities
- `.claude/skills/` - Reusable skills made of instructions plus optional scripts
- `.tmp/` - Temporary generated outputs
- [.gitignore](/home/abdur-rafay/claude-code/.gitignore:1) - Local ignore rules for workspace-only files

## Current Agents

- [code-reviewer.md](/home/abdur-rafay/claude-code/.claude/agents/code-reviewer.md:1)
- [email-classifier.md](/home/abdur-rafay/claude-code/.claude/agents/email-classifier.md:1)
- [qa.md](/home/abdur-rafay/claude-code/.claude/agents/qa.md:1)
- [research.md](/home/abdur-rafay/claude-code/.claude/agents/research.md:1)
- [tell-me-the-time.md](/home/abdur-rafay/claude-code/.claude/agents/tell-me-the-time.md:1)

## Current Skills

- [design-website](/home/abdur-rafay/claude-code/.claude/skills/design-website/README.md:1) - Generate a premium one-page website mockup for a prospect

## How This Workspace Works

The design is simple:

1. `CLAUDE.md` defines the global defaults.
2. Agents handle focused, repeatable tasks.
3. Skills package instructions with scripts so execution is more reliable.
4. Specialized files can override the shared defaults when needed.

## Creating New Agents

Add a new markdown file under `.claude/agents/`.

Good agent files usually include:

- a clear purpose
- when to use the agent
- behavior rules
- useful commands or tools
- output expectations
- guardrails

## Creating New Skills

Add a folder under `.claude/skills/` with:

- `SKILL.md` for instructions
- `README.md` for human-facing setup and usage
- `scripts/` for deterministic helpers when needed

## Conventions

- Keep instructions practical and easy to scan.
- Prefer small, focused agents over giant all-purpose prompts.
- Put repeatable logic into scripts when possible.
- Document setup and usage close to the skill itself.
- Keep workspace-specific files out of version control when appropriate.

## Local Notes

- `.codex` is ignored in [.gitignore](/home/abdur-rafay/claude-code/.gitignore:1)
- Some skills may require local credentials, API keys, or OAuth setup
- Generated outputs should usually go into `.tmp/` unless a skill says otherwise

## Goal

This workspace is meant to be the central place where all Claude capabilities live together cleanly:
one shared brain, many focused agents, and reusable skills that can grow over time.
