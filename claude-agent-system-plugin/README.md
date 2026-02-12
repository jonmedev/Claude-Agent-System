# Claude Agent System Plugin

A Claude Code plugin with intelligent workflow orchestration, parallel agent coordination, and automated code review. Now powered by **topus v3.0**.

## Skills

### `/systemcc` - Intelligent Workflow Router
The **only command you need** for implementation tasks. Auto-analyzes task complexity, risk, and scope to select and execute the optimal workflow automatically.

```bash
/systemcc fix the login bug
/systemcc refactor the authentication system
/systemcc migrate all models to new ORM
```

Features:
- 3-dimensional task analysis (complexity, risk, scope)
- Two-phase decision engine with confidence scoring
- Lyra AI prompt optimization
- Automatic workflow selection (streamlined, full validation, phase-based, PRD-based)
- Triple code review
- Complete end-to-end execution

### `/pcc` - Parallel Claude Coordinator (topus v3.0)
The **plugin version of topus v3.0**. Dual-mode orchestrator with Sonnet scouts and Opus implementers.

```bash
/pcc implement user authentication with JWT tokens
/pcc --plan "analyze the payment system architecture"
/pcc --exec "add WebSocket support"
```

**v3.0 features included**: Dual-mode (PLAN/EXECUTE) with auto-detection, CPE (Codebase Pattern Extraction), CIA (Change Impact Analysis), DSVP (Domain-Specific Verification Profiles), confidence scoring, wave-based execution, signal bus, and adaptive timeouts.

Best for:
- Most development tasks
- Cost-conscious workflows
- When exploration speed matters

### `/pcc-opus` - PCC Opus Edition (topus v3.0)
Uses **Opus scouts** AND **Opus implementers** for maximum quality. Same v3.0 engine as `/pcc`.

```bash
/pcc-opus refactor the entire payment processing system
```

Best for:
- Critical production systems
- Complex architectural changes
- Unfamiliar codebases

### `/review` - Code Review Swarm
Deploys **6 parallel review agents** to analyze code, then **automatically fixes** CRITICAL and MAJOR findings with your approval. Fully self-contained - no external plugin dependencies.

```bash
/review                  # Review all uncommitted changes (default)
/review staged           # Review only staged changes
/review src/auth.ts      # Review specific file(s)
/review "auth module"    # Review files matching a description
```

Review agents deployed (all 6 run in parallel):

| Agent | Focus |
|-------|-------|
| Bug & Logic Reviewer | Security vulnerabilities, crashes, logic errors, resource leaks |
| Project Guidelines Reviewer | Style conventions, CLAUDE.md standards, best practices |
| Silent Failure Hunter | Swallowed exceptions, bad fallbacks, inadequate error handling |
| Comment Analyzer | Stale docs, misleading comments, missing documentation |
| Type Design Analyzer | Encapsulation, invariant expression, type safety |
| Test Coverage Analyzer | Test gaps, missing edge cases, test quality |

Features:
- **Self-contained agents** - all 6 agents defined as `.md` files in `.claude/agents/`, no external plugins needed
- **Health score** (0-10) with severity-weighted formula
- **Cross-agent correlation** - related findings from different agents grouped together
- **Deduplicated report** - orchestrator merges overlapping findings
- **Agent verdicts table** - quick pass/fail per agent
- **Opt-in fix phase** - parallel fix agents resolve CRITICAL and MAJOR findings (you choose: fix critical+major, fix all, or report only)

## Installation

```bash
/plugin marketplace add jonmedev/Claude-Agent-System
/plugin install pcc
```

## Skill Comparison

| Skill | Use Case | Engine | Agents | Modifies Code? |
|-------|----------|--------|--------|----------------|
| `/systemcc` | Any implementation task - auto-routes | Auto-selected | Auto-selected | Yes |
| `/pcc` | Dual-mode orchestration (v3.0) | topus v3.0 | SIMPLE ~8, MEDIUM ~15-22, COMPLEX ~22-35 | Yes (EXECUTE) / No (PLAN) |
| `/pcc-opus` | Max quality orchestration (v3.0) | topus v3.0 | SIMPLE ~8, MEDIUM ~15-22, COMPLEX ~22-35 | Yes (EXECUTE) / No (PLAN) |
| `/review` | Code review & analysis + fix | Review swarm | 6 review agents + 1-4 fix agents | Only if opted in |

## How It Works

### `/systemcc` Flow

1. **Detection** - Acknowledges command, shows Lyra AI optimization
2. **Analysis** - Two-phase decision engine scores complexity, risk, scope
3. **Selection** - Routes to optimal workflow with confidence scoring
4. **Execution** - Runs all phases automatically
5. **Review** - Triple code review (Senior Engineer, Lead Engineer, Architect)
6. **Complete** - Summary with session learnings

### `/pcc` and `/pcc-opus` Flow (topus v3.0)

Mode is auto-detected from intent, or forced with `--plan` / `--exec`.

1. **Mode Detection** - Auto-detects PLAN or EXECUTE from your request
2. **CPE** - Codebase Pattern Extraction (~30s, learns project conventions)
3. **Parallel Exploration** - Scout agents map the codebase (findings tagged HIGH/MEDIUM/LOW)
4. **CIA** - Change Impact Analysis with risk scoring (1-10)
5. **Synthesis** - Combines findings into unified understanding
6. **3-Resolution Plan Creation** - Strategic, Tactical, and Operational levels in `.claude/plans/{task}.md`
7. **User Review** - You edit and approve the plan _(PLAN mode stops here)_
8. **Wave-Based Implementation** - DAG-ordered parallel agents with signal bus
9. **DSVP Verification** - Domain-specific verification profiles + test strategy execution
10. **Simplification** - Parallel cleanup agents
11. **Final Report** - Summarizes everything

Complexity tiers: SIMPLE (~8 agents), MEDIUM (~15-22 agents), COMPLEX (~22-35 agents).

### `/review` Flow

1. **Scope Detection** - Determines what to review (uncommitted changes, staged, files, or description)
2. **Load Agents** - Reads 6 agent definition files from `.claude/agents/review-*.md`
3. **Review Swarm** - 6 specialized agents launch in parallel (same wall-clock time as 1)
4. **Synthesis** - Orchestrator deduplicates, cross-references, and scores findings
5. **Report** - Consolidated findings by severity (CRITICAL > MAJOR > MINOR) with health score
6. **Fix Findings** (opt-in) - Parallel fix agents resolve CRITICAL/MAJOR issues (grouped by file, exclusive ownership)

## License

MIT
