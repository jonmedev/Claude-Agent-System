# Implementation Plan: Topus Supremacy + URL Migration to jonmedev

Created: 2026-02-12
Status: PENDING APPROVAL
Orchestrator: Opus
Execution Mode: Parallel Agent Deployment (4 agents)

## Summary

Two combined objectives:
1. **Topus Supremacy**: Enhance topus.md with missing flags (--scout-model, --resume, --hotfix), Memory Bank integration, detection feedback, ecosystem references (/review, /cleanup-context, anti-yolo-web, PRD generation), and reposition topus as THE flagship command across all docs.
2. **URL Migration**: Replace all `Kasempiternal` → `jonmedev` across 6 files.

After this update, topus will be the definitive command that subsumes pcc-opus capabilities and is properly positioned as the flagship.

## Scope

### In Scope
- topus.md enhancements (new flags, new phases, ecosystem integration)
- PCC SKILL.md sync (mirror topus changes)
- URL migration (6 files, 13 instances)
- Positioning updates (help.md, QUICK_START.md, README.md, 04-WORKFLOW-SELECTION.md)

### Out of Scope
- pcc-opus/SKILL.md rewrite (stays as simplified alternative)
- systemcc modules themselves (they stay as-is)
- Other workflow files (anti-yolo-web, aidevtasks, etc. stay as-is)

## Parallelization Strategy

### Work Streams (4 agents, fully parallel)

| Stream | Focus | Files | Can Parallel With |
|--------|-------|-------|-------------------|
| A | topus.md enhancements | 1 file (topus.md) | B, C, D |
| B | URL migration (Kasempiternal → jonmedev) | 6 files | A, C, D |
| C | Positioning + doc updates | 4 files | A, B, D |
| D | PCC SKILL.md sync (AFTER Stream A) | 1 file | B, C |

### Dependencies
- Stream D depends on Stream A (must sync after topus.md is updated)
- Streams A, B, C are fully independent

---

## Stream A: Topus.md Enhancements

**Agent**: Opus
**File**: `.claude/commands/topus.md`
**Objective**: Add missing capabilities to make topus THE definitive command

### Changes to make (in order of where they appear in the file):

#### 1. New Flags in Frontmatter (top of file)
Update argument-hint to include new flags:
```yaml
argument-hint: <task description or --plan/--exec/--scout-model/--resume/--hotfix task description>
```

#### 2. Phase 0: Add Flag Parsing (after frontmatter, before Phase 0.1)
Add new **Phase 0.0: Flag Parsing & Mode Override** section:
```
Supported flags:
  --plan          Force PLAN mode (analysis only, no code)
  --exec          Force EXECUTE mode (full implementation)
  --scout-model [sonnet|opus]  Override exploration model (default: sonnet)
                               Use opus for critical systems / unfamiliar codebases
  --resume        Resume from last checkpoint in .claude/plans/
  --hotfix        Emergency mode: 1 agent, minimal checks, fast fix
```

#### 3. Phase 0.0.1: Resume Detection
If --resume flag is set:
- Scan .claude/plans/ for existing plan files
- Find most recent plan with incomplete phases
- Display plan summary and ask user to confirm resume point
- Skip to the appropriate phase
- Reuse existing Knowledge Bus, contracts, and signals

#### 4. Phase 1: Add Detection Feedback (beginning of Phase 1)
Add mandatory detection feedback at Phase 1 start:
```
🎯 TOPUS v3.0 DETECTED — Dual-mode orchestration initiated
✅ Reading project configuration and CLAUDE.md...
```

#### 5. Phase 1.3.1: Emergency Hotfix Detection (after Phase 1.3)
If --hotfix flag OR keywords "production down", "critical bug", "urgent hotfix":
- Override tier → ULTRA-SIMPLE
- Pipeline: 1 implementer, lint+type check only, no review
- Timeout: 5 minutes max
- Post-fix: Recommend full verification later

#### 6. Phase 1.5: Enhance Mode Detection with Web/PRD detection
After mode scoring, add:
- **Web Project Detection**: If task involves web UI + project is web (React/Vue/Angular/HTML), offer anti-yolo-web wireframe-first approach
- **PRD Detection**: If task uses "feature", "product", "requirements", offer PRD generation in PLAN mode

#### 7. Phase 2: Scout Model Override
In the exploration phase, update agent spawning to respect --scout-model flag:
- Default: Sonnet scouts (cost-efficient)
- With --scout-model opus: Opus scouts (maximum quality for critical/unfamiliar codebases)
- Display which model is being used for scouts

#### 8. Phase 7.5: Add /review Reference (after Phase 7, before Phase 8)
Add optional deep code review note:
```
## Phase 7.5: Optional Deep Code Review

For comprehensive code review with 6 specialized agents, consider running:
  /review [scope]

This deploys parallel reviewers for: Bug & Logic, Project Guidelines, Silent Failures,
Comment Quality, Type Design, and Test Coverage. Can auto-fix CRITICAL/MAJOR findings.

Skip this phase if Phase 7 triple review found no MAJOR issues.
```

#### 9. Phase 9: Add /cleanup-context Reference (end of Phase 9)
Add to final report:
```
If continuing to work in this session, consider running `/cleanup-context`
to optimize context before starting the next task.
```

#### 10. Phase 10: Add Memory Bank Integration (enhance existing Phase 10)
After post-mortem, add Memory Bank update step:
```
## Phase 10.2: Memory Bank Update (Optional)

If session produced significant learnings:
- Update CLAUDE-patterns.md with new patterns discovered
- Update CLAUDE-decisions.md with architecture choices made
- Update CLAUDE-troubleshooting.md with issues resolved and solutions
- Capture user corrections in CLAUDE-dont_dos.md

Only update if files exist in project. Do NOT create them if absent.
Ask user permission before writing to memory files.
```

#### 11. Appendix D: Flag Reference (new appendix after Appendix C)
Add complete flag reference:
```
## Appendix D: Flag Reference

| Flag | Effect | Example |
|------|--------|---------|
| --plan | Force PLAN mode | /topus --plan "analyze auth system" |
| --exec | Force EXECUTE mode | /topus --exec "add OAuth2" |
| --scout-model sonnet | Sonnet scouts (default, cost-efficient) | /topus --scout-model sonnet "task" |
| --scout-model opus | Opus scouts (maximum quality) | /topus --scout-model opus "critical migration" |
| --resume | Resume from last checkpoint | /topus --resume |
| --hotfix | Emergency fast-track mode | /topus --hotfix "fix production crash" |
```

---

## Stream B: URL Migration (Kasempiternal → jonmedev)

**Agent**: Opus
**Objective**: Replace all `Kasempiternal` with `jonmedev` across 6 files

### Files and changes:

1. **`README.md`** (5 instances)
   - Line 17: `/plugin marketplace add Kasempiternal/...` → `jonmedev/...`
   - Line 28: `curl ... Kasempiternal/...` → `jonmedev/...`
   - Line 31: `curl ... Kasempiternal/...` → `jonmedev/...`
   - Line 37: `irm ... Kasempiternal/...` → `jonmedev/...`

2. **`setup-claude-agent-system.sh`** (1 instance)
   - Line 16: `REPO_URL="https://github.com/Kasempiternal/..."` → `jonmedev/...`

3. **`setup-claude-agent-system.ps1`** (1 instance)
   - Line 32: `$REPO_URL = "https://github.com/Kasempiternal/..."` → `jonmedev/...`

4. **`claude-agent-system-plugin/plugin.yaml`** (2 instances)
   - Line 4: `author: "Kasempiternal"` → `author: "jonmedev"`
   - Line 5: `repository: "...Kasempiternal/..."` → `jonmedev/...`

5. **`claude-agent-system-plugin/README.md`** (1 instance)
   - Line 84: `/plugin marketplace add Kasempiternal/...` → `jonmedev/...`

6. **`.claude-plugin/marketplace.json`** (2 instances)
   - Line 6: `"name": "Kasempiternal"` → `"name": "jonmedev"`
   - Line 7: `"url": "https://github.com/Kasempiternal"` → `"url": "https://github.com/jonmedev"`

### Verification:
- `grep -r "Kasempiternal" .` returns 0 results (excluding .git/)
- `curl -sI https://raw.githubusercontent.com/jonmedev/Claude-Agent-System/main/setup-claude-agent-system.sh` returns HTTP 200

---

## Stream C: Positioning Updates (Topus as Flagship)

**Agent**: Opus
**Objective**: Reposition topus as THE flagship command across all user-facing docs

### Files and changes:

#### 1. `.claude/commands/help.md`
- Change "RECOMMENDED" from /systemcc to /topus
- Update opening line: "**Just use `/topus "your task"`** — The flagship dual-mode orchestrator"
- Keep /systemcc listed but as "auto-router (delegates to workflows)" not "RECOMMENDED"
- Update decision guide line 170: "Always start with `/topus`" instead of "/systemcc"
- Add note: "For quick auto-routing, /systemcc detects and delegates to the right workflow"

#### 2. `.claude/QUICK_START.md`
- Change "Primary Command" from /systemcc to /topus with v3.0 description
- Move /systemcc to "Auto-Router" subsection below topus
- Keep both commands visible but topus is primary

#### 3. `README.md`
- Update "When to Use Each Command" table:
  - "Most tasks (simple to complex)" → `/topus` (auto-detects mode)
  - "Quick auto-routing" → `/systemcc` (picks workflow for you)
  - Keep complex/architecture rows pointing to /topus
- Update /systemcc section header: "Auto-Router" instead of "The main command"
- Ensure /topus section comes BEFORE /systemcc in document order (if not already)

#### 4. `.claude/commands/systemcc/04-WORKFLOW-SELECTION.md`
- Update topus from "Domain + Fallback" to "Flagship Orchestrator"
- Add note: "topus is the recommended command for direct invocation; systemcc routes TO topus when appropriate"

---

## Stream D: PCC SKILL.md Sync

**Agent**: Opus
**Depends on**: Stream A completion
**File**: `claude-agent-system-plugin/skills/pcc/SKILL.md`
**Objective**: Sync with updated topus.md (change name: pcc in frontmatter, keep rest identical)

### Process:
1. Wait for Stream A to complete
2. Copy topus.md content to SKILL.md
3. Update frontmatter: name: pcc, description: "Parallel Claude Coordinator v3.0..."
4. Verify line count matches

---

## Verification

After all streams complete:
- [ ] No remaining "Kasempiternal" references (grep check)
- [ ] curl URLs resolve for jonmedev repo (HTTP 200)
- [ ] topus.md has --scout-model, --resume, --hotfix flags
- [ ] topus.md has Memory Bank integration (Phase 10.2)
- [ ] topus.md has detection feedback in Phase 1
- [ ] topus.md references /review and /cleanup-context
- [ ] help.md positions topus as flagship
- [ ] QUICK_START.md shows topus as primary command
- [ ] README "When to Use" table favors topus
- [ ] PCC SKILL.md synced with updated topus.md

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| topus.md grows too large | Medium | Low | Keep additions concise, link to docs for details |
| Positioning change confuses existing users | Low | Low | Keep /systemcc available, just reposition |
| PCC sync misses changes | Low | Medium | Full copy + frontmatter swap |

---
**USER: Please review this plan. Edit any section directly in this file, then confirm to proceed.**
