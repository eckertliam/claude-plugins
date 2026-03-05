---
name: devplan
description: Use when creating, reading, or updating a development plan. Triggers on "plan", "make a plan", "create a plan", when starting a multi-step task, or when a plan file already exists in the working directory.
---

# Devplan

Manage development plans as persistent markdown files in the current working directory.

## Invocation

### `/devplan [filename] [task description]`

Parse $ARGUMENTS to determine:
- **Filename**: If an argument looks like a filename (e.g., ends in `.md`, or is a slug like `auth-plan`), use it. Append `.md` if missing.
- **Task description**: Everything else is the task/goal.
- **If no filename given**: Derive one from the task (e.g., "build auth system" -> `auth-system-plan.md`).
- **If no arguments at all**: Search for existing plan files (`*plan*.md`, `PLAN.md`) in the cwd. If found, read and resume. If multiple, list them and ask which to work from. If none, ask the user what to plan.

## Creating a Plan

**Before writing the plan, build domain knowledge:**

1. Explore the codebase — read the project structure, key config files (package.json, Cargo.toml, etc.), entry points, and existing patterns
2. Read files directly relevant to the task
3. Understand the tech stack, conventions, and constraints

**Then write the plan file:**

```markdown
# Plan: [Goal]

## Overview
What we're building/doing and why. Key context from codebase exploration.

## Steps
- [ ] Step 1: Description
  - [ ] Sub-step 1a
  - [ ] Sub-step 1b
- [ ] Step 2: Description

## Decisions
<!-- Record architectural and implementation decisions with rationale -->

## Notes
<!-- Constraints, blockers, open questions -->
```

Keep steps concrete and actionable. Each step should be something you can sit down and do, not a vague category. Prefer 5-15 top-level steps — split into sub-steps for complexity.

## Working from a Plan

When a plan file exists and you're doing related work:

1. Read the plan file at the start of the task
2. Identify the next unchecked step
3. Do the work
4. **Update the plan file** after completing each step:
   - Check off completed steps: `- [ ]` -> `- [x]`
   - Add sub-steps if a step turned out more complex than expected
   - Record decisions made in the Decisions section
   - Add context or blockers to Notes
5. Never remove steps — mark as skipped with a note if no longer needed

## Auto-invocation Guidance

When working on a multi-step task, check if a plan file exists in the cwd. If one does, read it and orient your work around it. Update it as you progress.
