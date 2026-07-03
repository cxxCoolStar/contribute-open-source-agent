# Core Agent PR Workflow

Use this reference after a repository or opportunity has been selected.

## Issue Screening

Screen open issues for:

- Labels such as `bug`, `enhancement`, `help wanted`, `good first issue`, eval/test labels, agent/tool/context labels, or close project-specific equivalents.
- Activity within the last 60 days when possible.
- No assignee. Exclude assigned issues unless the assignee or a maintainer explicitly invites outside help.
- Clear expected behavior, reproduction steps, failing scenario, or acceptance criteria.
- Likely change scope of 1-3 files.
- A direct relationship to core agent behavior.

Exclude issues if they are docs-only, UI-only, setup-only, dependency-only, or generic cleanup.


## Assignee Check

Before recommending an issue, inspect assignee metadata and recent comments:

1. Check the issue `assignees` list and visible assignee in GitHub UI or API.
2. Read recent comments for ownership signals such as `assigned to me`, `I can take this`, `working on it`, `will fix`, or maintainer assignment language.
3. If the issue has an assignee, exclude it unless the assignee or a maintainer explicitly says outside help is welcome.
4. If the issue is unassigned but someone claims it in comments, treat it as assigned and exclude it.

Use one of these values:

- `clean: unassigned and no ownership claim found`
- `risky: unclear ownership, ask before coding`
- `exclude: assigned or claimed`

## PR Collision Check

Before recommending any issue, prove it is not already being handled:

1. Prefer GitHub search qualifiers that exclude linked PRs when available, for example `is:issue is:open no:assignee -linked:pr`.
2. Open the issue and inspect linked PR/development metadata.
3. Check timeline or events for cross-referenced, connected, mentioned, or closed-by PRs.
4. Search open PRs in the same repository for the issue number, title keywords, and phrases such as `fixes #123`, `closes #123`, `resolves #123`, or `addresses #123`.
5. Read recent comments for ownership signals: `I am working on this`, `I opened a PR`, `see #456`, `fixed in`, `pending release`, or maintainer assignment language.

Use one of these values:

- `clean: no linked/open PR found`
- `risky: abandoned/stale PR exists, needs maintainer comment first`
- `exclude: active PR or maintainer-owned work exists`

## Repository Analysis Prompt

```markdown
# Core Agent Contribution Analysis

GitHub repository: {REPO_URL}
My stack: {USER_STACK}
Goal: Find 1-3 PR directions that improve or test core agent behavior within {TIMEBOX}.

## Preparation

Read these files if present:
- README.md
- CONTRIBUTING.md
- Package and test configuration
- Main agent entry files
- Tool routing/execution files
- Context, memory, permission, eval, and orchestration files

Then output the directory structure to depth 3, mark likely core agent modules, and describe the core agent loop in 2-3 sentences.

## Opportunity Screening

For each candidate, include:
- Source: issue or code-analysis gap
- Core agent behavior affected
- Entry files
- Expected effort
- Assignee check
- PR collision check
- Test strategy
- Acceptance risk
- Interview value

Exclude peripheral work.
```

## Technical Design Prompt

```markdown
# Technical Design

Repository: {REPO_URL}
Prior analysis:
- Core architecture: {SUMMARY}
- Selected contribution direction: {DIRECTION}
- Core files: {FILES}
- Current gap: {GAP}

Before designing, reread the core files and confirm the current implementation.

## Boundaries

**Core agent behavior:** {ONE_SENTENCE}
**Out of scope:** 2-3 bullets, including any peripheral areas intentionally ignored
**Success criteria:** observable or testable outcomes
**Constraints:**
- Preserve backward compatibility
- Avoid new dependencies unless explicitly approved
- Keep the PR small, ideally under about 300 changed lines

## Options

Provide 2-3 options. For each:
- Core idea
- Integration points
- Data flow or state transition
- Pros
- Risks
- Best fit

Compare options by complexity, intrusion, extensibility, acceptance chance, and interview value.

## Implementation Plan

List modified files, ordered steps, tests, manual verification, and edge cases.

## Maintainer Comment

Draft a concise professional English comment under 150 words:
1. Objective agent-behavior problem
2. Proposed direction
3. Ask whether maintainers would accept this PR or already have plans
```

## Implementation Guardrails

Before writing code:

- Read every file to be changed.
- Inspect formatter, lint, type, and test configuration.
- Confirm the main branch can run, or document why not.

Implementation principles:

- Implement in small verifiable steps.
- Prefer extension over invasive rewrites.
- Preserve public API and existing behavior outside the selected core agent behavior.
- Avoid new dependencies unless clearly justified and approved.
- Match existing naming, typing, comments, and test style.

Stop for the user when:

- Scope expands outside core-agent work.
- Compatibility cannot be preserved.
- A new dependency is needed.
- Two viable designs require product or maintainer judgment.

## PR Draft Template

```markdown
## Problem

{Describe the current core agent behavior problem objectively.}

## Solution

{Describe the chosen approach and why it fits the existing architecture.}

## Changes

- {Change 1}
- {Change 2}
- {Change 3}

## Testing

- `{COMMAND}` - {RESULT}

## Notes for Reviewer

{Design decisions, tradeoffs, or files worth reviewing closely.}
```

Title format:

```text
{type}({scope}): {short description}
```

Common types: `fix`, `feat`, `test`, `refactor`. Prefer `test` only when the PR adds coverage for core agent behavior.

## Interview Narrative

Use the actual contribution artifacts, not generic claims:

- Context: what the repository's agent does and why this module mattered.
- Contribution: what behavior was fixed, protected, or tested.
- Process: 3-5 technical decisions and why each was made.
- Result: PR status, tests, files changed, measurable impact if available, and maintainer feedback.
- Challenges: 1-2 real difficulties and how they were resolved.
- Capabilities shown: architecture reading, test design, API compatibility, agent evaluation, tool routing, context management, or maintainer communication.