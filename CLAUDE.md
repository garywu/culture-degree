# Claude AI Development Guide - Culture Degree

This file tracks AI-assisted development sessions for the Culture Degree educational platform project.

## 🎓 Project Overview

**Project Name**: Culture Degree  
**Type**: Educational Platform (Web Application)  
**Status**: Initial Development  
**Repository**: https://github.com/garywu/culture-degree  

### Mission Statement
Culture Degree transforms cultural learning into structured, degree-like programs, democratizing cultural education through comprehensive learning paths that explore diverse traditions, histories, and contemporary practices.

### Current Project State
- **Phase**: Architecture Planning & Setup
- **Git Repository**: Initialized
- **External Dependencies**: 5 submodules integrated
- **Project Management**: 10 GitHub issues created

### Development Priorities
1. Define technology stack and architecture
2. Design core data models for educational content
3. Plan user authentication and progress tracking
4. Create responsive UI/UX design system
5. Implement content management system

## Current Session Information

- **Date**: 2025-06-25
- **Session ID**: [Run `make session-start` to begin]
- **Session Type**: Initial Setup
- **Primary Goals**: 
  - [x] Initialize project with agent-init
  - [x] Set up GitHub repository
  - [x] Create project management issues
  - [ ] Define technology stack
  - [ ] Plan system architecture

### Session Context
- **Previous Session**: N/A (First session)
- **Key Decisions Made**: 
  - Using agent-init for professional development standards
  - Issue-driven development workflow
  - Manual release strategy starting at v0.0.1
- **Next Steps**: Architecture and technology decisions

## 🛠️ Intelligent Commands

### Project Analysis & Intelligence
```bash
# Run project analysis
./scripts/project-detector.sh          # Analyze project characteristics
./scripts/setup-analyzer.sh           # Comprehensive setup analysis
make analyze                          # Quick project health check
make health                           # Full health assessment
```

### Smart Development Commands
```bash
# Context-aware development (adapts to project type)
make dev                # Start development server (auto-detected)
make test               # Run tests (framework-specific)
make build              # Build project (optimized for project type)
make lint               # Run linters (language-specific)
make format             # Format code (language-specific)

# Intelligent project management
make session-start      # Start tracked development session
make session-status     # Show current session status
make session-end        # End session with summary
make session-log MSG="description"  # Log session activity
```

### Git Workflow (Enhanced)
```bash
# Issue-driven development
gh issue list           # View all issues
gh issue create         # Create new issue with templates
gh pr create            # Create pull request with analysis

# Smart git operations
make git-status         # Multi-repo status (if applicable)
make git-cleanup        # Clean up branches and optimize
git tag -l              # List all versions
```

### Framework-Specific Commands
Based on your project type, additional commands are available:

#### For Web Applications
```bash
make dev-web            # Start web development server
make build-web          # Build for production
make preview            # Preview production build
make lighthouse         # Run Lighthouse performance audit
```

#### For APIs
```bash
make dev-api            # Start API development server
make test-api           # Run API integration tests
make docs-api           # Generate API documentation
make db-migrate         # Run database migrations
```

#### For Libraries
```bash
make build-lib          # Build library for distribution
make publish            # Publish to package registry
make docs-lib           # Generate library documentation
```

## 🔄 Enhanced Workflow Procedure

### 1. Session Initialization
- **Start with analysis** - Run `make analyze` to understand current project state
- **Review project intelligence** - Check the Project Intelligence section above
- **Initialize session** - Use `make session-start` for tracked development
- **Set clear goals** - Define specific, measurable session objectives

### 2. Intelligent Planning Phase
- **Leverage project analysis** - Use detected project type for context-appropriate planning
- **Create GitHub issues** for all planned work with project-specific templates
- **Add analysis context** to issues (reference project type, frameworks, maturity score)
- **Get framework-specific guidance** from detected technologies
- **Wait for approval** before proceeding with implementation

### 3. Smart Issue Creation
- Use descriptive titles with appropriate prefixes and project context:
  - `[BUG]` for bug fixes (include affected framework/component)
  - `[FEAT]` for new features (specify if frontend/backend/fullstack)
  - `[DOCS]` for documentation (specify if API/user/developer docs)
  - `[REFACTOR]` for code refactoring (mention performance/maintainability)
  - `[TEST]` for test additions/modifications (unit/integration/e2e)
  - `[CHORE]` for maintenance tasks (dependency updates/tooling)
  - `[SECURITY]` for security-related changes
  - `[PERF]` for performance improvements

### 4. Context-Aware Development Process
1. **Select an issue** from the backlog with project type in mind
2. **Review project analysis** for relevant context and constraints
3. **Plan implementation** using framework-specific best practices
4. **Get approval** on approach with architectural considerations
5. **Implement solution** following detected project patterns
6. **Run health checks** - Use `make health` to verify changes
7. **Update session log** - Use `make session-log MSG="progress update"`
8. **Create PR** with analysis context and framework-specific testing

### 4. Pull Request Guidelines
- Reference the issue number in PR description
- Include test results
- Ensure all checks pass
- Request review when ready
- Use conventional commits for automatic versioning

### 5. Release Management

#### Manual Release Strategy (Recommended)
For full control over versioning, use manual-only releases:
- Start at `v0.0.1` and increment deliberately
- No automated version bumps or scheduled releases
- Create releases only when significant changes are ready
- See [Release Management Guide](https://github.com/garywu/claude-init/blob/main/docs/release-management-manual.md)

#### Automated Release Strategy (Alternative)
For projects preferring automation:
- **main**: Active development
- **beta**: Beta releases (manual trigger)
- **stable**: Stable releases (manual trigger)

#### Conventional Commits
Use these prefixes for semantic versioning:
- `feat:` New feature (minor version bump)
- `fix:` Bug fix (patch version bump)
- `feat!:` or `BREAKING CHANGE:` (major version bump)
- `docs:`, `style:`, `refactor:`, `test:`, `chore:` (no release)

## Active Issues

| Issue # | Title | Status | Priority |
|---------|-------|--------|----------|
| #1      | [Example] | Planning | High |

## Completed Issues

| Issue # | Title | PR # | Date Completed |
|---------|-------|------|----------------|
| -       | -     | -    | -              |

## Project Structure

```
.
├── src/                 # Source code
├── tests/              # Test files
├── docs/               # Documentation
├── scripts/            # Utility scripts
├── .github/            # GitHub configuration
│   ├── workflows/      # CI/CD workflows
│   └── ISSUE_TEMPLATE/ # Issue templates
├── CLAUDE.md           # This file
├── README.md           # Project documentation
├── CONTRIBUTING.md     # Contribution guidelines
├── CODE_OF_CONDUCT.md  # Code of conduct
└── SECURITY.md         # Security policy
```

## Development Environment

### Available Tools
The following CLI tools are available and should be used:

- **Search & Navigation**: `rg`, `fd`, `ag`, `fzf`, `broot`
- **File Operations**: `eza`, `bat`, `sd`, `lsd`
- **Git Operations**: `gh`, `lazygit`, `delta`, `tig`, `gitui`
- **Development**: `tokei`, `hyperfine`, `watchexec`
- **Data Processing**: `jq`, `yq`, `gron`, `jless`

### Key Configurations
- **Linting**: ShellCheck, YAML lint, Markdown lint, Python (flake8, black)
- **Pre-commit hooks**: Configured in `.pre-commit-config.yaml`
- **CI/CD**: GitHub Actions workflows for testing and deployment
- **Version**: Following Semantic Versioning (starting at 0.0.1)
- **Release Channels**: main (dev), beta (weekly), stable (monthly)

## 📊 Project Health & Intelligence Tracking

### Health Indicators
- **Last Health Check**: [Timestamp]
- **Overall Health Score**: [0-100]
- **Critical Issues**: [Count of critical issues]
- **Security Status**: [Secure/Warning/Critical]
- **Performance Status**: [Optimal/Warning/Needs Attention]
- **Documentation Coverage**: [Complete/Partial/Missing]

### Intelligence Updates
- **Project Type Changes**: [Track evolution]
- **Framework Additions**: [New technologies adopted]
- **Complexity Growth**: [Monitor codebase growth]
- **Dependency Health**: [Track security and updates]

## 🎯 Session Management & Analytics

### Current Session Metrics
- **Session Duration**: [Auto-tracked]
- **Files Modified**: [Auto-counted]
- **Commands Executed**: [Track development commands]
- **Issues Worked**: [Link to GitHub issues]
- **Health Score Change**: [Before/after comparison]

### Notes for Next Session
- [ ] Initialize Next.js project with TypeScript
- [ ] Set up Prisma with PostgreSQL
- [ ] Configure tRPC routers
- [ ] Implement authentication with NextAuth.js
- [ ] Create component library structure
- [ ] Set up CI/CD pipeline (Issue #3)

### Continuous Improvement Tracking
- **Code Quality Trend**: [Improving/Stable/Declining]
- **Test Coverage Trend**: [Improving/Stable/Declining]
- **Security Posture Trend**: [Improving/Stable/Declining]
- **Performance Trend**: [Improving/Stable/Declining]

## 📈 Session History & Intelligence Evolution

### Previous Sessions
| Date | Session ID | Project Type | Health Score | Key Accomplishments |
|------|------------|--------------|--------------|-------------------|
| 2025-06-25 | 2025-06-25_14:21:05_92385 | Web App | N/A | Initial setup, Architecture design |

### Project Evolution Timeline
| Date | Change Type | Description | Impact |
|------|-------------|-------------|--------|
| -    | -           | -           | -      |

## 🧠 Claude AI Assistant Configuration

### Project-Specific AI Guidance
Based on detected project characteristics, Claude will:
- **Prioritize suggestions** for [detected project type] development
- **Use framework patterns** from [detected frameworks]
- **Apply security practices** appropriate for [detected technologies]
- **Suggest performance optimizations** for [detected architecture]

### Adaptive Assistance Level
- **Beginner**: Detailed explanations and step-by-step guidance
- **Intermediate**: Balanced guidance with code examples
- **Advanced**: High-level architectural guidance and best practices
- **Expert**: Code review and optimization suggestions

*Current Level*: [Auto-detected based on project maturity and complexity]

---

**🚀 Enhanced by Claude-Init Intelligence System**

Remember: Leverage project analysis, maintain session tracking, and let intelligence guide your development decisions!