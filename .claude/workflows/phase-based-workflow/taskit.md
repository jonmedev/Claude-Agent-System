# Phase-Based Task Execution System

> **Note**: This phase-based approach is powered by **topus v3.0** and accessed via `/topus` (script install) or `/pcc` (plugin install), or automatically through `/systemcc` routing for large-scope tasks.

## ⚠️ File Policy
Temporary phase files go to `.claude/temp/` and are deleted after workflow completion.
Do NOT create files in the target repo unless user explicitly requests.

## Overview

Phase-based development breaks complex tasks into focused phases, optimizing context usage and improving quality by allowing deep focus on each phase independently. Access this workflow via `/topus` for explicit phase planning.

### Dual-Mode Operation (v3.0)

Topus v3.0 supports two modes, **auto-detected** from intent:

- **PLAN mode** -- Exploration and analysis only. Produces a strategy document at `.claude/plans/{task}.md` and stops. Force with `--plan`.
- **EXECUTE mode** -- Full implementation pipeline including wave-based parallel execution and DSVP verification. Force with `--exec`.

### v3.0 Systems Active During Phase Execution

- **CPE (Codebase Pattern Extraction)** -- Learns project conventions (naming, architecture, patterns) in ~30 seconds before any planning begins
- **Confidence Scoring** -- All exploration findings are tagged HIGH / MEDIUM / LOW to prioritize what matters
- **CIA (Change Impact Analysis)** -- Every proposed change receives a risk score (1-10) before implementation
- **Signal Bus** -- Agents communicate discoveries in real time during wave-based implementation
- **DSVP (Domain-Specific Verification Profiles)** -- Tailored verification for auth, database, API, frontend, infra, data, and testing domains
- **Adaptive Timeouts** -- SIMPLE 3 min/agent, MEDIUM 8 min, COMPLEX 15 min
- **Conditional Phase Skipping** -- Smart skip logic saves ~8 agents on SIMPLE tasks

### Critical for Large Codebases
When working in projects with hundreds of files or when context accumulates during long sessions, Claude's context window can become compressed, leading to:
- Degraded code quality
- Missed important details
- Superficial implementations
- Errors from forgotten context

Phase-based execution solves this by resetting context between phases while maintaining continuity through documentation.

## Core Concept

Instead of attempting to complete an entire complex task in one go (which can overwhelm context and reduce quality), phase-based execution:

1. **Decomposes** the task into logical phases
2. **Documents** each phase in a structured plan
3. **Executes** phases sequentially with focused context
4. **Maintains** continuity through phase documentation

### Why This Matters
- **Context Window Limit**: Claude has a finite context window (~200k tokens)
- **Quality Degradation**: Performance drops significantly when context is compressed
- **Large Projects**: In codebases with 100+ files, context fills quickly
- **Solution**: Phase-based execution keeps each phase under 30k tokens

## How It Works

### 1. Task Analysis & Planning (v3.0 Enhanced)
When invoked with `/topus "your complex task"`, the system:
- **CPE** runs first to learn project conventions (~30 seconds)
- Scouts explore the codebase in parallel, with findings tagged HIGH/MEDIUM/LOW
- **CIA** produces risk scores (1-10) for all proposed changes
- Breaks the task into phases via **3-resolution planning** (Strategic, Tactical, Operational)
- Creates a `.claude/plans/{task-slug}.md` file with detailed phase descriptions
- Estimates complexity and assigns a tier (SIMPLE ~8 agents, MEDIUM ~15-22, COMPLEX ~22-35)
- In **PLAN mode**, execution stops here with the strategy document

### 2. Phase Execution (Wave-Based in v3.0)
In **EXECUTE mode**, for each wave of phases:
- DAG determines execution order (phases with no unmet dependencies run in parallel)
- **Signal bus** enables inter-agent communication during implementation
- Each agent receives only relevant context for its scope
- **Adaptive timeouts** apply based on tier (3/8/15 min per agent)
- Documents outcomes in .claude/temp/
- **Conditional phase skipping** bypasses unnecessary phases for SIMPLE tasks

### 3. Verification (DSVP in v3.0)
- **DSVP** selects domain-specific verification profiles (auth, database, API, frontend, infra, data, testing)
- Automated **test strategy generation** with coverage targets
- Each verification profile applies domain-relevant checks

### 4. Context Optimization
- Each phase starts fresh with minimal context
- Previous phase outcomes are summarized
- Only essential information carries forward
- Reduces token usage by 60-80%

### Context Management Strategy
```
Traditional Approach:
- Start: 10k tokens
- After exploring: 30k tokens
- After implementing: 60k tokens
- After testing: 80k tokens (compressed, degraded quality)

Phase-Based Approach:
- Phase 1: 10k tokens (fresh start)
- Phase 2: 12k tokens (fresh start + summary)
- Phase 3: 11k tokens (fresh start + summary)
- Phase 4: 10k tokens (fresh start + summary)
Total: 43k tokens with consistent quality
```

## Usage

```bash
/topus "build a complete user dashboard with analytics, notifications, and settings"
```

This creates a phase plan and begins execution:

```
Phase 1: Architecture & Setup
Phase 2: Analytics Components
Phase 3: Notification System
Phase 4: Settings Panel
Phase 5: Integration & Testing
```

## Implementation Structure

### Files Created

All phase-based workflow files are created in `.claude/` directories:

1. **`.claude/plans/{task-slug}.md`** - Master plan with all phases
2. **`.claude/temp/phase-1-outcome.md`** - Results from Phase 1
3. **`.claude/temp/phase-2-outcome.md`** - Results from Phase 2
4. **...continuing for each phase**
5. **Final summary** in the plan file or conversation

### Phase Plan Template

```markdown
# Task: [Task Description]
Date: [Current Date]
Total Phases: [Number]

## Phase 1: [Phase Name]
**Objective**: Clear, focused goal for this phase
**Inputs**: 
- Required files/context
- Dependencies from previous phases
**Outputs**:
- Expected deliverables
- Documentation updates
**Success Criteria**:
- Specific, measurable outcomes
**Estimated Time**: [X] minutes

## Phase 2: [Phase Name]
[Similar structure...]

## Execution Notes
- Phases can be executed sequentially
- Each phase should be self-contained
- Context from previous phases is summarized, not fully loaded
```

### Phase Outcome Template

```markdown
# Phase [X] Outcome: [Phase Name]
Completed: [Timestamp]

## Accomplished
- Specific achievement 1
- Specific achievement 2

## Key Decisions
- Decision 1 and rationale
- Decision 2 and rationale

## Modifications Made
- File: path/to/file - Description of changes
- File: path/to/file2 - Description of changes

## Handoff to Next Phase
Critical information for Phase [X+1]:
- Important context point 1
- Important context point 2

## Learnings
- Pattern discovered
- Optimization identified
```

## Execution Flow

```python
def execute_topus(task_description):
    # 1. Analyze and Plan
    phases = analyze_task_complexity(task_description)
    create_task_plan(phases)  # Creates in .claude/temp/

    # 2. Execute Each Phase
    for phase in phases:
        # Minimal context load
        context = load_phase_context(phase)

        # Focused execution
        results = execute_phase(phase, context)

        # Document outcomes in .claude/temp/
        save_phase_outcome(phase, results)

        # Prepare handoff
        handoff = prepare_handoff(results)

    # 3. Final Summary and Cleanup
    create_task_summary(all_phase_outcomes)
    cleanup_temp_files()  # Delete .claude/temp/ files
```

## Benefits

1. **10x Context Efficiency**: Each phase uses minimal tokens
2. **Higher Quality**: Deep focus on one aspect at a time
3. **Better Error Recovery**: Issues isolated to phases
4. **Clear Progress**: Visible phase completion
5. **Knowledge Capture**: Structured documentation
6. **Convention Awareness (v3.0)**: CPE auto-learns project patterns before planning
7. **Risk Visibility (v3.0)**: CIA scores every change 1-10 before implementation
8. **Domain-Specific Verification (v3.0)**: DSVP applies targeted checks per domain
9. **Real-Time Agent Coordination (v3.0)**: Signal bus enables inter-agent communication during waves

## Integration with Existing Workflows

### Automatic Selection via /systemcc
`/systemcc` will automatically use phase-based execution (via topus v3.0 patterns) when:
- Current context exceeds 30,000 tokens
- More than 10 files are loaded in context
- Working in a project with 100+ files and broad changes
- Task is estimated to take 60+ minutes
- Multiple system integrations are involved

### Manual Usage
`/topus` (script) or `/pcc` (plugin) can be used directly for:
- **PLAN mode** -- Exploration and strategy only (`--plan` flag)
- **EXECUTE mode** -- Full implementation pipeline (`--exec` flag, or auto-detected)
- **Planning** complex features before implementation
- **Large tasks** that would overwhelm single-context execution
- **Refactoring** that touches many files
- **Migrations** requiring systematic changes

## Example: Complex Feature Implementation

```bash
User: /topus "implement complete authentication system with OAuth, 2FA, and session management"
```

Generated Plan:
```
Phase 1: Database Schema & Models
- User model with auth fields
- Session tracking tables
- OAuth provider configs

Phase 2: Core Authentication Logic
- Password hashing
- Session generation
- Token management

Phase 3: OAuth Integration
- Provider setup (Google, GitHub)
- Callback handling
- Token exchange

Phase 4: Two-Factor Authentication
- TOTP implementation
- Backup codes
- Recovery flow

Phase 5: Frontend Integration
- Login/Register forms
- OAuth buttons
- 2FA screens

Phase 6: Validation & Security
- Manual validation
- Integration validation
- Security audit
```

## Advanced Features

### Wave-Based Parallel Execution (v3.0)
In v3.0, parallel execution is automatic via DAG analysis. The system builds a dependency graph and deploys agents in waves -- all phases in a wave run simultaneously, and the next wave starts when the current one completes. The signal bus allows agents within a wave to share discoveries in real time.

Phases can still be annotated manually for clarity:
```markdown
## Phase 3: Component A [PARALLEL-OK with Phase 4]
## Phase 4: Component B [PARALLEL-OK with Phase 3]
```

### Phase Dependencies
Explicit dependency declaration:
```markdown
## Phase 5: Integration
**Depends on**: Phase 2, Phase 3 outcomes
**Blocks**: Phase 6
```

### Checkpoint Recovery
If execution fails, resume from last completed phase by referencing the plan:
```bash
/topus --resume "continue from phase 3"
```

## Best Practices

1. **Phase Size**: Each phase should be 15-45 minutes of work
2. **Clear Boundaries**: Phases should have minimal overlap
3. **Documentation**: Always document key decisions
4. **Testing**: Include test phases for complex features
5. **Handoffs**: Make phase transitions explicit

## Limitations

- Not suitable for simple, single-file tasks
- Requires upfront planning time
- Best for tasks taking >1 hour total
- May create overhead for tiny features

## Success Metrics

Typical improvements with phase-based execution (enhanced by v3.0):
- 60-80% reduction in context usage
- 2-3x improvement in code quality
- 90% reduction in context-related errors
- 50% faster completion for complex tasks
- ~8 agents saved on SIMPLE tasks via conditional phase skipping (v3.0)
- Domain-specific verification coverage via DSVP profiles (v3.0)