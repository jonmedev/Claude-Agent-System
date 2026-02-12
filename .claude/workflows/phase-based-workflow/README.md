# Phase-Based Workflow System

> **Powered by topus v3.0** -- This workflow is the execution backbone of the `/topus` and `/pcc` commands. All v3.0 features (dual-mode, CPE, CIA, DSVP, confidence scoring, wave-based execution, signal bus) are available when this workflow is invoked.

## Introduction

The Phase-Based Workflow is a development methodology that dramatically improves Claude Code's effectiveness on complex tasks by breaking them into focused, sequential phases. This approach addresses the context window limitations and maintains high quality throughout large projects.

## Why Phase-Based Development?

### The Problem
When tackling complex tasks in a single attempt:
- Context window fills with unnecessary information
- Quality degrades as the task progresses  
- Errors compound across the implementation
- Claude loses track of earlier decisions
- Testing and validation become superficial

### The Solution
Phase-based development:
- Breaks complex tasks into manageable phases
- Each phase operates with minimal, focused context
- Quality remains consistently high
- Errors are isolated to specific phases
- Clear progress tracking and documentation

## Core Principles

### 1. **Decomposition First**
Before coding, decompose the task into logical phases. Each phase should:
- Have a single, clear objective
- Be completable in 15-45 minutes
- Produce concrete deliverables
- Build upon previous phases

### 2. **Context Minimization**
Each phase starts with only essential context:
- Phase objective and scope
- Summary of previous phase outcomes
- Only relevant code files
- Specific patterns to follow

### 3. **Documentation as Handoff**
Each phase ends with structured documentation:
- What was accomplished
- Key decisions and rationale
- Critical information for next phase
- Lessons learned

### 4. **Progressive Enhancement**
Phases build incrementally:
- Phase 1: Foundation and structure
- Phase 2-N: Feature implementation
- Final Phase: Integration and polish

## Workflow Structure (topus v3.0)

With v3.0, the workflow supports **dual-mode operation**: PLAN mode produces a strategy document and stops; EXECUTE mode runs the full pipeline below. Mode is auto-detected from intent or overridden with `--plan` / `--exec`.

```
/topus "complex task description"
    │
    ├── Mode auto-detection (PLAN or EXECUTE)
    │
    ├── CPE: Codebase Pattern Extraction (~30s)
    │   └── Auto-learns naming, architecture, and conventions
    │
    ├── Parallel exploration with confidence scoring
    │   └── Findings tagged HIGH / MEDIUM / LOW
    │
    ├── CIA: Change Impact Analysis (risk 1-10)
    │
    ├── Creates 3-resolution implementation plan
    │   └── Strategic → Tactical → Operational
    │   └── .claude/plans/{task-slug}.md
    │
    │   [PLAN mode stops here]
    │
    ├── Wave-based execution (DAG-ordered)
    │   ├── Signal bus for inter-agent communication
    │   ├── Adaptive timeouts (3/8/15 min per tier)
    │   └── Conditional phase skipping for simple tasks
    │
    ├── DSVP verification (domain-specific profiles)
    │   └── auth, database, API, frontend, infra, data, testing
    │
    └── Simplification + final summary
```

## Benefits Demonstrated

### Traditional Approach
```
Task: "Build complete user dashboard"
- Attempts everything at once
- Context: 50,000+ tokens
- Quality degrades after 30%
- Errors in authentication affect charts
- Testing is superficial
- Result: 60% functional, needs rework
```

### Phase-Based Approach
```
Task: "Build complete user dashboard"
Phase 1: Architecture & Layout (8,000 tokens)
Phase 2: Authentication Integration (6,000 tokens)
Phase 3: Chart Components (7,000 tokens)
Phase 4: Real-time Updates (5,000 tokens)
Phase 5: Testing & Polish (4,000 tokens)
- Total: 30,000 tokens (40% reduction)
- Each phase at 100% quality
- Errors isolated and fixed immediately
- Result: 100% functional, well-tested
```

## When to Use Phase-Based Workflow

### Ideal For:
- Features requiring 1+ hours of work
- Multi-file architectural changes
- Complex integrations
- Full-stack features
- Major refactoring
- System migrations

### Not Recommended For:
- Simple bug fixes
- Single-file changes
- Tasks under 30 minutes
- Straightforward updates

## Integration with Agent System

The phase-based workflow complements existing agents and is the core execution engine for topus v3.0:

1. **With `/topus` (v3.0)**: Primary execution mode -- full dual-mode pipeline with CPE, CIA, DSVP, wave execution, and signal bus
2. **With `/pcc` (v3.0)**: Plugin equivalent -- same v3.0 engine, installed via plugin system
3. **With Complete System**: Each phase can use full agent workflow
4. **With Orchestrated**: Phases can be executed via orchestrated agents
5. **With /systemcc**: Can delegate phase execution to appropriate workflow

## Best Practices

### 1. Phase Planning
- **3-7 phases** optimal for most tasks
- **Clear boundaries** between phases
- **Logical progression** from foundation to completion
- **Testable outcomes** for each phase

### 2. Context Management
- **Summarize, don't carry** full context forward
- **Document decisions** with rationale
- **Highlight blockers** immediately
- **Keep handoffs concise** but complete

### 3. Quality Gates
- **Test each phase** before proceeding
- **Validate assumptions** early
- **Fix issues immediately** in current phase
- **Document patterns** for reuse

## Common Patterns

### Frontend Feature Pattern
```
Phase 1: Component Structure & State
Phase 2: API Integration  
Phase 3: UI Implementation
Phase 4: Error Handling & Loading States
Phase 5: Testing & Optimization
```

### Backend Service Pattern
```
Phase 1: Data Models & Schema
Phase 2: Core Business Logic
Phase 3: API Endpoints
Phase 4: Authentication & Authorization
Phase 5: Testing & Documentation
```

### Full-Stack Feature Pattern
```
Phase 1: Database Schema & Models
Phase 2: Backend Services
Phase 3: API Layer
Phase 4: Frontend Components
Phase 5: Integration & Testing
Phase 6: Performance & Polish
```

## Measuring Success

Phase-based development typically achieves:
- **60-80% context reduction**
- **2-3x quality improvement**
- **50% faster completion** for complex tasks
- **90% fewer context-related errors**
- **100% documentation coverage**

## Getting Started

1. Use the phase-based planning command:
   ```bash
   /topus "implement complete search functionality with filters"
   ```

2. Or let `/systemcc` automatically route to phase-based execution:
   ```bash
   /systemcc "refactor entire API layer"
   ```

3. Watch phases execute with focused precision

## Advanced Usage

### Parallel Phases
Mark phases that can run simultaneously:
```markdown
Phase 3: API Implementation [PARALLEL-OK with Phase 4]
Phase 4: UI Components [PARALLEL-OK with Phase 3]
```

### Phase Dependencies
Explicitly declare dependencies:
```markdown
Phase 5: Integration Testing
Depends on: Phase 2, Phase 3 completion
Blocks: Phase 6
```

### Checkpoint Recovery
Resume from specific phase by referencing the plan file:
```bash
/topus --resume "continue from phase 3"
```

## Troubleshooting

### Common Issues

1. **Phase Too Large**
   - Solution: Break into sub-phases
   - Target: 15-45 minutes per phase

2. **Lost Context Between Phases**
   - Solution: Improve handoff documentation
   - Include: Key decisions, file locations, patterns used

3. **Circular Dependencies**
   - Solution: Restructure phases
   - Ensure: Clear progression path

## Delivered in v3.0

The following previously planned enhancements are now available:

- **AI-powered phase generation** -- CPE auto-learns conventions, CIA scores risk, 3-resolution planning auto-generates phases
- **Automatic complexity scoring** -- Confidence scoring (HIGH/MEDIUM/LOW) on all exploration findings, plus CIA risk scores (1-10)
- **Collaborative phase execution** -- Signal bus enables real-time inter-agent communication during wave-based execution

## Future Enhancements

- Phase template library
- Integration with CI/CD

## Conclusion

Phase-based development transforms how Claude Code handles complex tasks. With topus v3.0, phases are now enhanced with CPE pattern extraction, CIA risk analysis, confidence-scored exploration, wave-based parallel execution, and domain-specific verification via DSVP. Start using `/topus` (or `/pcc` via the plugin) today for your complex development tasks.