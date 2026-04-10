# OpenCode Agent System

## Overview

This file defines the main agent orchestration workflow. All subagents are automatically invoked by the main agent as needed.

## Main Agent Workflow

When you receive a feature request requiring research or implementation:

```
Feature Request
    │
    ├──► seed-researcher ──────► .agent/research/{topic}-seed.md
    │       (Initial problem understanding via AI agent)
    │
    ├──► web-search-researcher ──► .agent/research/
    │       (Deep research with verified sources)
    │
    ├──► task-planner ─────────► .agent/task/
    │       (PRD or implementation plan)
    │
    ├──► system-documenter ───► .agent/system/
    │       (New architecture/endpoints)
    │
    ├──► sop-logger ───────────► .agent/sops/
    │       (Mistakes or lessons learned)
    │
    └──► update-doc reindex ───► .agent/readme.md
            (Always run at end)
```

## Subagent Reference

| Subagent | Purpose | Output |
|----------|---------|--------|
| `seed-researcher` | Initial research via AI agent | `.agent/research/{topic}-seed.md` |
| `web-search-researcher` | Deep research with verified sources | `.agent/research/{topic}-*.md` |
| `task-planner` | Create PRDs and implementation plans | `.agent/task/{name}.md` |
| `system-documenter` | Update architecture/API docs | `.agent/system/{name}.md` |
| `sop-logger` | Log procedures and mistakes | `.agent/sops/{name}.md` |
| `update-doc` | Maintain .agent structure | Auto-updates readme.md |

## Research Format

All research MUST use standardized 3-file format in `.agent/research/`:

1. `{topic}-summary.md` - Executive summary, key findings, actionable insights
2. `{topic}-sources.md` - Full citations with URLs and reliability scores
3. `{topic}-examples.md` - Verified code examples with confidence scores

Reference: `.config/opencode/agents/web-search-researcher.md`

## Auto-Orchestration Rules

1. **Always run `update-doc reindex` at the end** - Keeps readme.md fresh
2. **Research first** - Before implementation, research the topic
3. **Log lessons** - If mistakes happen, invoke sop-logger
4. **Update docs** - If architecture changes, invoke system-documenter

## Quick Commands

```bash
# Rebuild readme navigation
/update-doc reindex

# Check for broken links
/update-doc link-check
```

---

Updated: 2026-03-16
