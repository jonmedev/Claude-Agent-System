# /help - Claude Agent System Help

## Quick Start

**Just use `/topus "your task"`** — The flagship dual-mode orchestrator that handles everything from quick fixes to complex refactors.

## All Available Commands

### 🎯 Auto-Router Command

#### `/systemcc` - Intelligent Workflow Router
Auto-router with Lyra AI optimization that selects the best workflow:
- **Agent OS** - Project initialization and standards
- **AI Dev Tasks** - PRD-based feature development
- **Phase-Based** - Large context management
- **Complete System** - 6-agent validation workflow
- **Orchestrated** - Quick 3-agent execution

```bash
/systemcc "implement user authentication"  # Auto-selects workflow
/systemcc --workflow=agetos "setup project"  # Force specific workflow
```

### 🚀 Specialized Workflows

#### `/agetos` - Agent OS Project Standards
Comprehensive project initialization and standardization.
- Setup coding standards and conventions
- Configure development tools and workflows
- Establish team practices

```bash
/agetos init  # Full project setup
/agetos analyze  # Analyze current state
```

#### `/aidevtasks` - PRD-Based Development
Structured feature development with requirements.
- Create Product Requirement Documents
- Generate hierarchical task lists
- Implement with approval checkpoints

```bash
/aidevtasks "build notification system"
/aidevtasks create-prd "user dashboard"
```

### 🔧 Core Workflows

#### `/orchestrated` - Streamlined 3-Agent Workflow
Quick execution for simple tasks.
- Agent O: Orchestrator
- Agent D: Developer  
- Agent R: Reviewer

```bash
/orchestrated "fix button styling"
```

#### Complete System (6 Sequential Agents)
For complex tasks requiring thorough validation, `/systemcc` automatically runs:
1. Strategic analysis phase
2. Implementation phase
3. Quality verification phase
4. Functional testing phase
5. Documentation phase
6. Version control phase

### 🛠️ Workflow Access

All workflows are accessed through `/systemcc` which automatically:
- Detects task complexity
- Selects appropriate workflow
- Runs all agents sequentially
- No manual agent commands needed

### 🚀 Flagship Command

#### `/topus` v3.0 - Flagship Dual-Mode Orchestrator
Intelligent system with two modes: **PLAN** (analysis/exploration, no code changes) and **EXECUTE** (full implementation pipeline).

**Mode Auto-Detection:** The system infers mode from your intent. Manual override with `--plan` or `--exec` flags.

- **PLAN mode** - Deep codebase analysis, architecture exploration, confidence-scored findings (no code modifications)
- **EXECUTE mode** - Wave-based parallel agent execution with 3-resolution planning (Strategic/Tactical/Operational)
- **DSVP** - Domain-Specific Verification (auth, database, API, frontend, etc.)
- **CIA** - Change Impact Analysis with risk scoring
- **CPE** - Codebase Pattern Extraction (learns project conventions)
- **Confidence Scoring** - Exploration findings tagged HIGH/MEDIUM/LOW
- **Adaptive Tiers** - SIMPLE (~8 agents), MEDIUM (~15-22), COMPLEX (~22-35)

```bash
# PLAN mode (auto-detected from analysis intent)
/topus "analyze how our auth system works"
/topus --plan "explore database schema dependencies"

# EXECUTE mode (auto-detected from implementation intent)
/topus "add OAuth2 to the API"
/topus --exec "refactor database layer for better performance"
```

**Workflow:**
1. Task Understanding - Clarify requirements, auto-detect mode
2. Parallel Exploration - Multiple agents explore architecture, features, dependencies, tests
3. Hypothesis Verification - Read and verify findings with confidence scoring
4. Plan Creation - Generate detailed plan in `~/.claude/plans/`
5. User Confirmation - Wait for approval before implementing (EXECUTE mode)
6. Wave-Based Execution - Dependency-ordered parallel agents (EXECUTE mode)

### 🔍 Utility Commands

#### `/analyzecc` - Auto-Adapt to Your Stack
Analyzes your project and adapts the agent system to your tech stack.
- Detects language, frameworks, and tools
- Updates agent commands to match your stack
- Perfect for Python AI/ML, React, Rails, etc.

```bash
/analyzecc
```

## Decision Guide

```
Don't know which to use?
    ↓
**Start with /topus** for direct dual-mode orchestration,
or /systemcc for automatic workflow routing.

/topus handles:
- Architecture analysis → PLAN mode (auto-detected)
- Complex refactors, migrations → EXECUTE mode (auto-detected)
- Quick fixes, simple changes → EXECUTE mode (auto-detected)
- Override with --plan or --exec flags

/systemcc auto-routes to:
- Project setup → Agent OS (/agetos)
- Feature building → AI Dev Tasks (/aidevtasks)
- Complex validation → Complete system
- Quick fixes → Orchestrated
- Large context / deep planning → Topus

Manual override:
/systemcc --workflow=[agetos|aidevtasks|complete|orchestrated]
```

## Context Management

`/systemcc` automatically uses phase-based execution (via `/topus`) when:
- Current context > 30k tokens
- Project has 100+ files
- Task touches 5+ modules
- Estimated time > 60 minutes

## Examples

See `/help examples` or check `commands/examples.md` for detailed scenarios.

## 🎯 Key Features

### Universal Lyra Optimization
ALL commands now use AI prompt enhancement:
- Transforms vague requests into detailed specs
- Ensures complete code delivery
- Optimizes for each workflow type

### Intelligent Routing
`/systemcc` analyzes:
- Task complexity and type
- Current context size
- Project characteristics
- Best workflow selection

## Tips

1. **Start with `/topus`** for direct dual-mode orchestration, or `/systemcc` for automatic workflow routing
2. **Building features?** Let it route to AI Dev Tasks
3. **New project?** It'll suggest Agent OS
4. **Large context?** Automatic phase-based execution
5. **Know what you want?** Use direct commands

## Workflow Temp Files

Temporary files needed during workflows (like inter-agent communication) are stored in `~/.claude/temp/` and automatically deleted after workflow completion.

## Learn More

- `.claude/commands/` - Command documentation
- `.claude/workflows/` - Workflow implementations
- `README.md` - Complete system guide