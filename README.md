# Documentation Brain Template

A reusable template for building an **AI-assisted documentation brain** — a structured set of markdown files that LLMs can use for context-aware assistance across teams.

## What Is a Documentation Brain?

A documentation brain is a curated folder of markdown files that serves as the single source of truth for project planning. It's designed to be:

- **Read by LLMs** — structured so AI tools can find, cross-reference, and reason about your project
- **Authored by humans** — planning files are written and maintained by your team
- **Synced from external tools** — design docs (Notion), task tracking (ClickUp/Jira), and other sources can be ingested
- **Extended with skills** — slash commands that automate common workflows (syncing, reporting, gap analysis)

## What's In This Template

| File | Purpose |
|------|---------|
| `project-charter.md` | Architecture rules, file structure, and principles for LLMs and humans |
| `ONBOARDING.md` | Step-by-step guide for populating a new brain |
| `EXAMPLES.md` | Usage examples: running skills, authoring specs, creating new skills |
| `planning/` | Skeleton templates for all planning files |
| `.claude/commands/` | Example skill template |

## Quick Start

1. Read `project-charter.md` to understand the architecture
2. Follow `ONBOARDING.md` to populate your brain
3. Reference `EXAMPLES.md` for interaction patterns
4. Copy skeleton files from `planning/` and fill in your project specifics

## Prerequisites

- **Claude Code** (or another LLM tool that reads local files)
- **Git** — the brain lives in a repo for version control and team access
- **Notion MCP** (optional) — for syncing design docs from Notion
- A project with teams, milestones, and features to document

## Design Philosophy

This template is opinionated. It's built around principles learned from real production use:

- **One source of truth per concept** — never duplicate authoritative data across files
- **Planning is human-authored, views are generated** — AI can synthesize and report, but humans own the plans
- **Skills are focused** — each skill does one job well, flags problems outside its scope
- **Structure enables AI** — consistent file formats let LLMs find and reason about your project reliably
