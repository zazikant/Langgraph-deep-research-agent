## Spec: Auto-Initialize .agent/ Structure on First Sub-Agent Use

### Current State
- `/update-doc init` exists as manual command
- Sub-agents expect `.agent/` to exist before creating files
- User wants seamless auto-initialization

### Required Changes

#### 1. Add `init-agent-structure` Helper Function
Create shared initialization logic that all sub-agents can call:

**File:** `.factory/droids/lib/init-agent.sh` or inline in each droid

```bash
# Pseudocode for init logic
def ensure_agent_structure():
    if not exists(".agent/"):
        create_dir(".agent/task")
        create_dir(".agent/system") 
        create_dir(".agent/sops")
        create_dir(".agent/research")
        create_file(".agent/readme.md", TEMPLATE_CONTENT)
        log("Auto-created .agent/ structure")
```

#### 2. Update Each Sub-Agent Droid

**research-delegator.md:**
```markdown
## Pre-Flight Check
Before research, ensure `.agent/` exists:
1. Check if `.agent/research/` is writable
2. If not, auto-run init logic
3. Log: "Auto-initialized .agent/ structure for project [project_name]"
```

**task-planner.md:**
```markdown
## Pre-Flight Check  
Before creating PRD, ensure `.agent/` exists:
1. Check if `.agent/task/` is writable
2. If not, auto-run init logic
3. Log: "Auto-initialized .agent/ structure"
```

**system-documenter.md:**
```markdown
## Pre-Flight Check
Before documentation, ensure `.agent/` exists:
1. Check if `.agent/system/` is writable
2. If not, auto-run init logic
```

**sop-logger.md:**
```markdown
## Pre-Flight Check
Before logging SOP, ensure `.agent/` exists:
1. Check if `.agent/sops/` is writable  
2. If not, auto-run init logic
```

#### 3. Update `/update-doc init`
Make it idempotent - safe to run multiple times:
- If `.agent/` exists: report "Already initialized, run `reindex` to refresh"
- If missing: create structure as before

#### 4. Project Detection
When auto-creating, detect project name:
- From `package.json` name field
- From git repo name
- From directory name
- Or prompt: "Project name for .agent/readme.md?"

### User Experience

**Scenario: New Project**
```
User: "Create a Next.js auth system"
Main Agent: [invokes task-planner]
task-planner: "Auto-initialized .agent/ structure for project 'my-app'"
task-planner: [creates PRD at .agent/task/PRD-auth.md]
```

**No manual /update-doc init needed - happens automatically.**

### Files to Modify
1. `research-delegator.md` - Add pre-flight check section
2. `task-planner.md` - Add pre-flight check section  
3. `system-documenter.md` - Add pre-flight check section
4. `sop-logger.md` - Add pre-flight check section
5. `update-doc.md` - Make init idempotent

### Implementation Notes
- Each droid is independent - include init logic inline
- Should support nested projects (monorepo) - check pwd first
- Log all auto-initializations for transparency