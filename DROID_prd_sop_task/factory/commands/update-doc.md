# /update-doc Command

## Usage
```
/update-doc <action> [options]
```

## Actions

### `init` - Initialize .agent/ Structure
Creates the full `.agent/` folder structure with navigation readme.

```bash
/update-doc init
```

**Creates:**
- `.agent/readme.md` - Navigation hub
- `.agent/task/` - Implementation plans
- `.agent/system/` - Architecture docs  
- `.agent/sops/` - Procedures & mistakes
- `.agent/research/` - Deep research outputs

---

### `reindex` - Fix Navigation Links
Scans all `.agent/` subfolders and rebuilds the readme.md navigation.

```bash
/update-doc reindex
```

**What it does:**
- Reads all files in task/, system/, sops/, research/
- Extracts titles and summaries
- Regenerates readme.md Quick Links section
- Preserves manual edits outside Quick Links
- Adds timestamps

---

### `link-check` - Validate Cross-Links
Finds broken links between documents.

```bash
/update-doc link-check
```

**Reports:**
- `[BROKEN]` Links to non-existent files
- `[ORPHAN]` Files not linked from anywhere  
- `[MISSING]` Expected cross-links (e.g., Task without System reference)

---

### `merge-sops` - Consolidate Duplicate SOPs
Finds and merges overlapping SOP files.

```bash
/update-doc merge-sops --dry-run  # Preview
/update-doc merge-sops --execute   # Actually merge
```

**Merges by:**
- Similar titles (fuzzy match)
- Related topics
- Chronological proximity

---

### `archive` - Archive Completed Tasks
Moves completed PRDs to archive status.

```bash
/update-doc archive --older-than 30d
```

---

## Implementation Notes

This command is executed by the main agent when invoked. It should:

1. **Read** the current `.agent/` structure
2. **Analyze** what's broken/outdated/missing
3. **Report** findings to user
4. **Execute** fixes only with explicit confirmation

### Safety Rules
- Never delete files without confirmation
- Create backups before destructive operations
- Log all changes to `.agent/.update-doc.log`

### Output Format
```
/update-doc <action> complete.

Summary:
- Files scanned: X
- Fixed: Y
- Needs attention: Z

Log: .agent/.update-doc.log
```
