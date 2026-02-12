# Implementation Plan: Update Installation URLs to jonmedev Fork

Created: 2026-02-12
Status: PENDING APPROVAL
Orchestrator: Opus
Execution Mode: Single Agent (simple find-replace)

## Summary

Replace all references to `Kasempiternal/Claude-Agent-System` with `jonmedev/Claude-Agent-System` across 6 files (setup scripts, READMEs, plugin configs). Then verify the URLs resolve correctly on GitHub.

## Scope

### In Scope
- Replace `Kasempiternal` → `jonmedev` in all 6 files (13 instances)
- Verify GitHub URLs resolve (curl check)

### Out of Scope
- CONTRIBUTING.md (uses `yourusername` placeholder, not Kasempiternal)
- CHANGELOG.md (references centminmod, historical — not installation)
- .claude/settings.local.json (just domain permissions, no repo-specific URLs)

## Files to Update

### 1. `README.md` (5 instances)
- Line 17: `/plugin marketplace add Kasempiternal/...` → `jonmedev/...`
- Line 28: `curl -sSL https://raw.githubusercontent.com/Kasempiternal/...` → `jonmedev/...`
- Line 31: `curl -sSL https://raw.githubusercontent.com/Kasempiternal/...` → `jonmedev/...`
- Line 37: `irm https://raw.githubusercontent.com/Kasempiternal/...` → `jonmedev/...`

### 2. `setup-claude-agent-system.sh` (1 instance)
- Line 16: `REPO_URL="https://github.com/Kasempiternal/..."` → `jonmedev/...`

### 3. `setup-claude-agent-system.ps1` (1 instance)
- Line 32: `$REPO_URL = "https://github.com/Kasempiternal/..."` → `jonmedev/...`

### 4. `claude-agent-system-plugin/plugin.yaml` (2 instances)
- Line 4: `author: "Kasempiternal"` → `author: "jonmedev"`
- Line 5: `repository: "https://github.com/Kasempiternal/..."` → `jonmedev/...`

### 5. `claude-agent-system-plugin/README.md` (1 instance)
- Line 84: `/plugin marketplace add Kasempiternal/...` → `jonmedev/...`

### 6. `.claude-plugin/marketplace.json` (2 instances)
- Line 6: `"name": "Kasempiternal"` → `"name": "jonmedev"`
- Line 7: `"url": "https://github.com/Kasempiternal"` → `"url": "https://github.com/jonmedev"`

## Verification

After replacing:
- [ ] `grep -r "Kasempiternal" .` returns 0 results (excluding .git/)
- [ ] `curl -sI https://raw.githubusercontent.com/jonmedev/Claude-Agent-System/main/setup-claude-agent-system.sh` returns HTTP 200
- [ ] `curl -sI https://raw.githubusercontent.com/jonmedev/Claude-Agent-System/main/setup-claude-agent-system.ps1` returns HTTP 200
- [ ] JSON files remain valid

---
**USER: Please review this plan. Edit any section directly in this file, then confirm to proceed.**
