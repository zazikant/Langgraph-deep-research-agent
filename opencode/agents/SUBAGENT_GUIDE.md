# Subagent Usage Guide

Guidelines for when to automatically invoke subagents instead of handling tasks directly.

## Available Subagents

| Subagent | Purpose | Trigger Keywords |
|----------|---------|------------------|
| `explore` | Codebase exploration | "find where", "how does", "locate", "search codebase" |
| `web-search-researcher` | Live web research | "research", "latest", "current", "find information" |
| `worker` | Parallel bulk tasks | multiple independent changes, renaming |
| `general` | Complex multi-step | "build", "implement", "refactor", "create feature" |

## Decision Flow

1. **Codebase questions** → Use `explore` first to understand the code
2. **Information requiring live/web data** → Use `web-search-researcher`
3. **Simple questions** → Answer directly

## Automatic Triggers

- Any task starting with "Find", "Research", "What are the latest..." → `web-search-researcher`
- Any task asking about existing code structure → `explore`
- Any task needing verification from web/docs → `web-search-researcher`
