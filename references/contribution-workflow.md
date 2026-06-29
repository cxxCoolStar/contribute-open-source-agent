# AI Agent Open-Source Contribution Workflow

This reference distills the PDF "手把手教你为 AI Agent 开源项目做贡献" into operational checklists and reusable prompts.

## Repository Fitness

Use these signals when choosing a repository:

| Signal | Healthy Indicator |
|---|---|
| Domain fit | Strongly related to AI Agent systems, tools, orchestration, memory, evals, MCP, or agent UI |
| Stars | Enough public attention for interview value; default target is `stars:>1000` unless the user prefers smaller projects |
| Last commit | Activity in roughly the last month |
| Issues | Closed/open ratio greater than 1 is a good sign |
| PR response | Maintainers usually respond or merge within about 2 weeks |
| Release cadence | Monthly or quarterly releases |

Useful GitHub search query:

```text
topic:ai-agent stars:>1000 pushed:>{DATE_3_MONTHS_AGO}
```

Compute `DATE_3_MONTHS_AGO` dynamically as today's date minus 3 months in `YYYY-MM-DD` format before running the search.

## Issue Filters

Search labels:

```text
label:"good first issue"
label:"help wanted"
label:"bug"
label:"documentation"
label:"enhancement"
```

Prefer issues that match all or most of these:

- Open and active within the last 60 days.
- Unassigned.
- No recent comment says someone is already working on it.
- Clear expected behavior, reproducible steps, or concrete acceptance criteria.
- Likely touches 1-3 files.
- Does not require broad architecture redesign.

Contribution types from easiest to hardest:

1. Docs or translation.
2. Bug fix.
3. Tests for uncovered behavior.
4. New tool or integration, especially for Agent frameworks.
5. Core feature, only after discussion with maintainers.

## Repository Analysis Prompt

Use this shape when asking another agent or a fresh pass to analyze a repository:

```markdown
# Open-Source Contribution Analysis

GitHub repository: {REPO_URL}
My stack: {USER_STACK}
Goal: Find 1-3 PR directions that can be completed within {TIMEBOX} and explained clearly in interviews.

## Preparation

Read these files if present:
- README.md
- CONTRIBUTING.md
- CHANGELOG.md / HISTORY.md
- Package and test configuration
- Main entry files such as main.py, index.ts, app.py

Then output the directory structure to depth 3, mark likely core modules, and describe the core Agent loop and planning style in 2-3 sentences.

## Issue Screening

Screen open issues for:
- labels: good first issue, help wanted, bug, documentation, enhancement, or close project-specific equivalents
- activity within the last 60 days
- no assignee and no comment claiming ownership
- clear expected behavior or reproduction steps
- likely change scope of 1-3 files

Return:

| Issue # | Title | Type | Required Skill | Estimated Effort | Why Recommended |

## Final Top 3

For each recommendation:
- PR direction name
- Source: issue or code-analysis dimension
- Entry files
- Why it fits my stack
- Estimated effort: small / medium / large
- Interview value
- Acceptance risk
- Test strategy
```

## AI Agent Architecture Review

When issue labels are not enough, inspect these dimensions. Every claim must cite concrete files and functions.

### 1. Task Planning

Identify whether the project uses ReAct, plan-and-execute, chain-of-thought-like decomposition, or no explicit planning.

Check:

- Can tasks be decomposed into subtasks?
- Is there an explicit plan generation step?
- Does failure trigger replanning or immediate exit?
- Can plans be persisted for resume?
- If there is no planning layer, is a small planning abstraction plausible?

### 2. Multi-Agent Collaboration

Check:

- Is the system single-agent or multi-agent?
- If single-agent, is there a natural orchestrator/worker split?
- If multi-agent, are roles, protocols, and aggregation clear?
- Is state shared safely between agents?

### 3. Context Management

Check:

- What happens near token limits: hard truncation, rolling window, summary compression, or other strategy?
- Can compression lose tool call history or intermediate results?
- How is cross-turn history stored and read?
- Are system instructions, tool results, and conversation history handled differently?

### 4. Human-in-the-Loop

Check:

- Are high-risk operations gated by human confirmation?
- Is there checkpointing and resume support?
- Can human feedback influence later decisions without restarting?

### 5. Evaluation

Check:

- Is there an eval module, fixture set, or trajectory-level test?
- Are final outputs only tested, or are tool calls and parameters evaluated?
- Is LangSmith, Arize, or a custom pipeline integrated?
- What is the smallest useful eval pipeline the project could accept?

### 6. Tool Retrieval and Routing

Check:

- Are all tool schemas injected globally, or are tools retrieved on demand?
- If there are more than about 20 tools, is vector or semantic retrieval used?
- Are tool descriptions clear enough to avoid selection confusion?
- Is MCP supported? If not, can the existing tool layer accept an MCP adapter?

### 7. Streaming and Intermediate Visibility

Check:

- Is token streaming supported?
- Are current subtask, tool name, parameters, and intermediate state externally visible?
- Is there an event or subscription API for frontends?
- Can streaming and status broadcast be added with low intrusion?

For each dimension, output:

```markdown
**Current state:** file path + function/class
**Gap:** concrete problem or missing capability
**Impact:** high / medium / low
**Improvement direction:** 1-3 sentences
**Change scope:** estimated files and line scale
**Interview angle:** one sentence
```

## Technical Design Prompt

Use this before implementation:

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

**Core problem:** {ONE_SENTENCE}
**Out of scope:** 2-3 bullets
**Success criteria:** observable or testable outcomes
**Constraints:**
- Do not break the existing public API
- Keep compatibility with supported Python/Node versions
- Keep the PR as small as practical, ideally under about 300 changed lines

## Options

Provide 2-3 options. For each:
- Core idea
- Key abstractions or function signatures
- Data flow
- Integration points
- Pros
- Risks
- Best fit

Compare options by complexity, intrusion, extensibility, acceptance chance, and interview value.

## Implementation Plan

List new files, modified files, ordered steps, manual verification, unit tests, and edge cases.

## Maintainer Comment

Draft a concise professional English comment under 150 words:
1. Objective problem
2. Proposed direction
3. Ask whether maintainers would accept this PR or already have plans
```

## Implementation Guardrails

Before writing code:

- Read every file to be changed.
- Inspect style config such as `.eslintrc`, `pyproject.toml`, `ruff.toml`, formatter config, and test framework.
- Confirm the main branch can run, or document why not.

Implementation principles:

- Implement in small verifiable steps.
- Prefer extension over modification.
- Preserve backward compatibility.
- Avoid new dependencies unless clearly justified and approved.
- Match existing naming, comments, typing, and test layout.

Stop for the user when:

- Scope expands beyond the chosen plan.
- Compatibility cannot be preserved.
- A new dependency is needed.
- Two viable designs need a product or maintainer judgment.

Proceed and explain afterward when:

- Pseudocode needs local adaptation.
- Additional error handling is needed.
- Tests need minor shape changes to match project style.

## PR Draft Template

```markdown
## Problem

{Describe the current problem objectively.}

## Solution

{Describe the chosen approach and why.}

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

Common types: `feat`, `fix`, `refactor`, `test`, `docs`.

## Follow-Up

After opening a PR:

- Watch for maintainer review comments.
- Respond with concise reasoning and concrete patches.
- If there is no response after the user's wait period, draft a polite follow-up comment or email.
- Capture review feedback and the final PR status for interview narration.

## Interview Narrative

Use the actual contribution artifacts, not generic claims:

- Context: what the project does in the AI Agent ecosystem and why it was chosen.
- Contribution: one sentence saying what was implemented, fixed, tested, or documented.
- Process: 3-5 decisions, focusing on why each decision was made.
- Result: PR status, link, project impact, tests, measurable metric if available, and maintainer feedback.
- Challenges: 1-2 real technical difficulties, how they were debugged, and final resolution.
- Reflection: what would be improved next time in design, communication, or scope.
- Capabilities shown: 2-3 skills such as architecture reading, test design, API compatibility, Agent evaluation, MCP integration, or maintainer communication.