# Claude Agent System - Quick Start (10/10 Code Quality)

## Primary Command

Just use: `/topus "describe what you want to do"`

Topus v3.0 auto-detects whether to analyze (PLAN mode) or implement (EXECUTE mode).
Use `--plan` or `--exec` flags to override. Use `--scout-model opus` for critical systems.

Key capabilities:
1. **Dual-Mode Operation** - PLAN mode for analysis/exploration, EXECUTE mode for full implementation
2. **CPE (Codebase Pattern Extraction)** - Auto-learns your project conventions before planning
3. **CIA (Change Impact Analysis)** - Risk scoring (1-10) for every proposed change
4. **Wave-Based Execution** - Dependency-ordered parallel agents with signal bus
5. **DSVP Verification** - Domain-specific validation (auth, database, API, frontend)
6. **Confidence Scoring** - All findings tagged HIGH/MEDIUM/LOW

## Auto-Router (Alternative)

`/systemcc "describe what you want to do"` — Automatically selects the best workflow for your task.
Routes to topus, orchestrated, complete-system, or specialized workflows based on complexity.

The auto-router provides:
1. **3-Dimensional Analysis** - Evaluates complexity, risk, and scope for optimal workflow selection
2. **Build Configuration Detection** - Automatically detects and applies Makefile, CI/CD, and linting rules
3. **Intelligent Routing** - Selects optimal workflow based on decision algorithms
4. **Quality Assurance** - Validates all inputs, handles errors gracefully, and maintains production standards
5. **Performance Optimization** - Uses early termination, caching, and efficient pattern matching
6. **Transparent Reasoning** - Provides detailed decision explanations and alternative suggestions

## Examples

```bash
# PLAN mode (auto-detected from analysis intent)
/topus "analyze how our auth system works"
/topus --plan "explore database schema dependencies"

# EXECUTE mode (auto-detected from implementation intent)
/topus "add OAuth2 to the API"
/topus --exec "refactor database layer for better performance"

# Auto-router examples (delegates to appropriate workflow)
/systemcc "fix typo in login page"              # Routes to orchestrated
/systemcc "implement user authentication"       # Routes to complete system
/systemcc "refactor all API endpoints"          # Routes to topus
```

## Intelligent Features

### Decision Engine Transparency
- Real-time scoring across 3 dimensions (Complexity/Risk/Scope)
- Build configuration auto-detection and application
- Confidence levels and alternative workflow suggestions
- Performance metrics and optimization feedback
- Detailed reasoning for all workflow selections

### Quality Assurance
- Comprehensive input validation and sanitization
- Robust error handling with graceful fallbacks
- Performance-optimized execution with early termination
- Production-ready robustness and reliability

## Auto-Adaptation

- `/analyzecc` - Deep project analysis with quality standards
  - Auto-detects tech stack with enhanced pattern recognition
  - Configures quality checks and validation rules
  - Updates all commands with optimized parameters

## Manual Commands (Power Users)

- `/orchestrated` - Force streamlined 3-agent workflow with error handling
- `/planner` - Start complete 6-agent system with comprehensive validation
- `/analyzecc` - Deep project analysis with quality standards
- `/help` - Show enhanced command system

## Advanced Context Management

The system uses intelligent context load prediction:
- Monitors token usage and file complexity in real-time
- Predicts context growth using statistical models
- Automatically switches to phase-based execution when needed
- Maintains optimal performance through smart resource management

## File Organization

Temporary workflow files are stored in `~/.claude/temp/` during execution:
- `~/.claude/temp/wireframes/` - ASCII wireframes (Anti-YOLO workflow)
- `~/.claude/temp/analysis/` - Project analysis files
- `~/.claude/temp/standards/` - Standards framework files
- `~/.claude/temp/WORK.md` - Current workflow state

**IMPORTANT**: Documentation files are NOT auto-created in your project. They are only created when you explicitly request them.

See `CLAUDE.md` for complete guidelines.

Happy coding! 🚀
