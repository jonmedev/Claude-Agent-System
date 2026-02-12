# Implementation Plan: Topus v3.0 Full Integration & Documentation Update

Created: 2026-02-12
Status: PENDING APPROVAL
Orchestrator: Opus
Execution Mode: Parallel Agent Deployment (4 agents)

## Summary

Update the entire Claude-Agent-System repository so that all files (middleware, routing, commands, documentation, configs, setup scripts) reflect Topus v3.0 features (dual-mode PLAN/EXECUTE, DSVP, signal bus, CIA, confidence scoring, CPE, wave-based execution). After this update, a fresh clone/install will have everything working and properly documented.

## Scope

### In Scope
- Version bumps (plugin.yaml, marketplace.json, hook metadata)
- Middleware v3.0 awareness (workflow-suggestions, decision engine, lyra)
- Command help & routing updates (help.md, systemcc modules, QUICK_START)
- Main documentation (README.md, plugin README, workflow docs)
- Setup scripts (mention topus in output)
- Stale reference fix (execute_plan_opus → execute_topus)

### Out of Scope
- topus.md itself (already v3.0, 3,368 lines)
- pcc/SKILL.md (already synced)
- CHANGELOG.md historical entries
- Creating brand new documentation files (just update existing)
- The parent directory name "plan-opus" on disk

## Parallelization Strategy

### Work Streams (4 agents, fully parallel)

| Stream | Focus | Files | Can Parallel With |
|--------|-------|-------|-------------------|
| A | Version bumps + stale refs | 5 files | B, C, D |
| B | Middleware & routing v3.0 awareness | 4 files | A, C, D |
| C | Command help, QUICK_START, systemcc modules, setup scripts | 7 files | A, B, D |
| D | Main documentation (README, plugin README, workflow docs) | 4 files | A, B, C |

### Dependencies: NONE — all streams are fully independent.

---

## Stream A: Version Bumps & Stale References (5 files)

**Agent**: Opus
**Objective**: Update version numbers and fix one stale function name

### Files:

1. **`claude-agent-system-plugin/plugin.yaml`**
   - Change: `version: "2.0.0"` → `version: "3.0.0"`
   - Also update description to mention v3.0 features

2. **`.claude-plugin/marketplace.json`**
   - Change top-level: `"version": "1.0.0"` → `"version": "3.0.0"`
   - Change plugin entry: `"version": "1.0.0"` → `"version": "3.0.0"`
   - Update descriptions to mention v3.0

3. **`.claude/middleware/hooks/user-prompt-submit/auto-pattern-detection.md`**
   - Change HOOK_METADATA version: `2.0.0` → `3.0.0`
   - Change footer version reference: `2.0.0` → `3.0.0`

4. **`.claude/middleware/hooks/post-tool-use/file-change-tracker.md`**
   - Change HOOK_METADATA version: `2.0.0` → `3.0.0`
   - Change footer version reference: `2.0.0` → `3.0.0`

5. **`.claude/workflows/phase-based-workflow/taskit.md`**
   - Change: `execute_plan_opus` → `execute_topus` (line ~162)

---

## Stream B: Middleware & Routing v3.0 Awareness (4 files)

**Agent**: Opus
**Objective**: Update middleware files to understand and route for Topus v3.0 dual-mode and features

### Files:

1. **`.claude/middleware/workflow-suggestions.json`**
   - Update the "topus" entry to include:
     - `"modes": ["plan", "execute"]`
     - `"features": ["dual-mode", "DSVP", "signal-bus", "CIA", "CPE", "confidence-scoring"]`
     - Updated description mentioning v3.0
     - Plan mode trigger hints (analysis verbs, strategy markers)

2. **`.claude/middleware/simplified-decision-engine.md`**
   - Add mode-aware routing logic:
     - Analysis/exploration tasks → topus with PLAN mode
     - Implementation tasks → topus with EXECUTE mode
   - Add signal words that trigger PLAN mode routing
   - Reference Phase 1.5 Mode Detection from topus.md

3. **`.claude/middleware/lyra-universal.md`**
   - Add v3.0-specific optimization patterns for topus
   - Include CPE awareness (codebase pattern extraction)
   - Add mode-detection hint in Lyra output
   - Reference confidence scoring system

4. **`.claude/commands/systemcc/07-DECISION-ENGINE.md`**
   - Add PLAN mode routing indicators (analysis verbs, strategy markers)
   - Update topus reference to mention dual-mode
   - Add --plan/--exec flag awareness

---

## Stream C: Command Help, Quick Reference, SystemCC & Setup (7 files)

**Agent**: Opus
**Objective**: Update user-facing command documentation with v3.0 features

### Files:

1. **`.claude/commands/help.md`**
   - Update /topus description to include:
     - Dual-mode operation (PLAN vs EXECUTE)
     - `--plan` and `--exec` flags
     - Brief mention of v3.0 features (DSVP, signal bus, CIA, CPE)
     - Usage examples: `/topus "analyze auth system"` (PLAN) vs `/topus "add OAuth2"` (EXECUTE)

2. **`.claude/QUICK_START.md`**
   - Update /topus entry with v3.0 dual-mode description
   - Add quick examples of both modes
   - Mention key v3.0 features briefly

3. **`.claude/commands/systemcc/00-INDEX.md`**
   - Update topus description from "large scope (phase-based)" to include v3.0
   - Mention dual-mode capability

4. **`.claude/commands/systemcc/04-WORKFLOW-SELECTION.md`**
   - Add PLAN mode indicators to topus trigger conditions
   - Add analysis/exploration task routing to topus PLAN mode

5. **`.claude/commands/systemcc/06-EXAMPLES.md`**
   - Add topus v3.0 mode examples if not already present
   - Include PLAN mode example and EXECUTE mode example

6. **`setup-claude-agent-system.sh`**
   - Add topus to the "installed commands" output message
   - Mention v3.0 capabilities briefly

7. **`setup-claude-agent-system.ps1`**
   - Same as bash script: add topus to installation output

---

## Stream D: Main Documentation (4 files)

**Agent**: Opus
**Objective**: Update primary documentation with v3.0 information

### Files:

1. **`README.md`**
   - Update /topus section with v3.0 features:
     - Dual-mode (PLAN vs EXECUTE)
     - Mode auto-detection + manual flags
     - Key v3.0 systems (DSVP, signal bus, CIA, CPE, confidence scoring)
     - Updated agent count table (v3.0 tiers)
   - Add /cleanup-context to "Other Commands" section
   - Update version references to v3.0
   - Ensure the comparison table (/systemcc vs /topus vs /pcc) is current

2. **`claude-agent-system-plugin/README.md`**
   - Add mention of /pcc being the plugin version of topus v3.0
   - Add v3.0 feature highlights for the pcc skill
   - Update version references

3. **`.claude/workflows/phase-based-workflow/README.md`**
   - Add explicit reference to topus v3.0
   - Mention dual-mode operation
   - Reference v3.0 features (CPE, confidence scoring, wave-based execution)

4. **`.claude/workflows/phase-based-workflow/taskit.md`**
   - Update content with v3.0 mode awareness (beyond just the function rename from Stream A)
   - Add examples of PLAN vs EXECUTE mode
   - Reference CPE and confidence scoring

---

## Verification

After all 4 streams complete:
- [ ] No remaining "plan-opus" references (grep check)
- [ ] All version numbers say 3.0.0
- [ ] help.md mentions dual-mode and --plan/--exec
- [ ] README describes v3.0 features
- [ ] Setup scripts mention topus
- [ ] Middleware routes correctly for analysis tasks (PLAN mode)

---

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Agents conflict on taskit.md | Low | Low | Stream A does function rename only, Stream D does content update |
| Middleware JSON format broken | Low | Medium | Agent validates JSON after edit |
| README grows too large | Medium | Low | Keep v3.0 section concise, link to topus.md for details |

---
**USER: Please review this plan. Edit any section directly in this file, then confirm to proceed.**
