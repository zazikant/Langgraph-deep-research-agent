# Project Documentation Hub

> Last Updated: 2026-03-13

Welcome to the `.agent/` folder - your AI-friendly documentation system.

## Navigation

### [Task](./task/) - Implementation Plans
What needs to be built. PRDs and step-by-step implementation plans.

**Quick Links:**
- [none yet - add first PRD]

### [System](./system/) - Architecture & Structure
How things work. Schemas, APIs, project structure.

**Quick Links:**
- [none yet - add first system doc]

### [SOPs](./sops/) - Procedures & Lessons
What we've learned. Mistakes logged, procedures documented.

**Quick Links:**
- [none yet - add first SOP]

### [Research](./research/) - Deep Investigations
External knowledge. Verified research summaries.

**Quick Links:**
- [none yet - add first research topic]

---

## How to Use This System

### For Main Agents
1. **Check relevant folder** before starting work
2. **Read existing docs** for context
3. **Delegate to sub-agents** via Task tool (research-delegator, task-planner, etc.)
4. **Receive compact handoffs** - sub-agents return only essentials
5. **Main conversation stays lean** - details live in `.agent/`

### Available Sub-Agents
Invoke these via the Task tool:
- **research-delegator** - Deep research, returns compact summaries
- **task-planner** - Creates PRDs and implementation plans
- **system-documenter** - Analyzes and documents architecture
- **sop-logger** - Captures mistakes and procedures

### Document Relationships
```
Research → Informs → Task → Implemented per → System → Learned via → SOPs
                ↑                            ↓                        ↓
                └────────── Main Agent coordinates ──────────────────┘
```

---

## Maintenance

### Compact Command
Run after isolated task completion:
```bash
# (Handled automatically - sub-agents auto-compact after handoff)
```

### Update Document Structure
```
/readme.md (this file) updated:
- Last Updated: 2026-03-13
- Next review: When sub-agent creates new doc
```
