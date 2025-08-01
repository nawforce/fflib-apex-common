# Claude Code Setup & Commands

This document explains how to use the custom commands configured for this project with Claude Code.

## Overview

This project includes custom slash commands in the `.claude/commands/` directory that provide structured workflows for common development tasks. These commands help ensure consistent code quality and follow project best practices.

## Available Commands

### `/qnew` - Session Initialization

**Purpose**: Initialize Claude session with project standards

**What it does**:

- Reviews all best practices listed in CLAUDE.md
- Ensures code follows established conventions
- Prevents implementation until standards are understood
- Should be run at the start of each Claude session

**When to use**: At the beginning of every Claude Code session

**Usage**:

```
/qnew
```

### `/qplan` - Plan Review Phase

**Purpose**: Review and validate implementation plans

**What it does**:

- Analyzes similar parts of the codebase for consistency
- Ensures your plan introduces minimal changes
- Promotes code reuse and follows existing patterns
- Reviews plans after they've been created

**When to use**: After creating a plan, to validate it against codebase patterns

**Usage**:

```
/qplan
```

### `/qcode` - Implementation Phase

**Purpose**: Implement planned changes with quality assurance

**What it does**:

- Implements your planned changes
- Runs tests to ensure nothing breaks
- Applies standard formatting to new files
- Validates implementation quality

**When to use**: After planning (/qplan) and reviewing standards (/qnew)

**Usage**:

```
/qcode
```

### `/qcheck` - Code Review Phase

**Purpose**: Perform thorough code quality analysis

**What it does**:

- Analyzes every source file you added or changed
- Checks against CLAUDE.md Writing Functions Best Practices
- Validates Writing Tests Best Practices compliance
- Reviews Implementation Best Practices adherence
- Acts as a skeptical senior engineer review

**When to use**: After implementation, before committing changes

**Usage**:

```
/qcheck
```

### `/qgit` - Git Operations

**Purpose**: Commit and push changes with proper formatting

**What it does**:

- Adds all changes to staging
- Creates commits following Conventional Commits format
- Ensures commit messages don't reference Claude/Anthropic
- Pushes changes to remote repository

**When to use**: After code review (/qcheck) when ready to commit

**Usage**:

```
/qgit
```

## Recommended Workflow

Follow this sequence for best results:

1. **Initialize** → `/qnew` - Start each session by reviewing project standards
2. **Plan** → Create your implementation plan
3. **Validate** → `/qplan` - Review your plan against codebase patterns
4. **Implement** → `/qcode` - Write your code with testing and formatting
5. **Review** → `/qcheck` - Perform thorough quality analysis
6. **Commit** → `/qgit` - Create proper commits and push to remote

## Tips

- **Don't skip steps**: Each command builds on the previous one
- **Use in sequence**: The workflow is designed to catch issues early
- **Review feedback**: Pay attention to the analysis from `/qcheck`
- **Iterate if needed**: Run `/qcheck` again after making fixes

## Getting Help

- See [CLAUDE.md](CLAUDE.md) for detailed project guidance
- See [GUIDELINES.md](GUIDELINES.md) for coding standards
- Each command provides specific feedback to guide improvements
