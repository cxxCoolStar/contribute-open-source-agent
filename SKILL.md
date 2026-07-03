---
name: contribute-open-source-agent
description: Analyze a fixed pool of AI Agent open-source repositories, identify contribution opportunities in core agent behavior, design and implement focused PRs, and turn the contribution into interview-ready evidence. Use when the user wants to contribute to an AI Agent repository, analyze core agent modules, find or implement a PR direction, draft maintainer communication, or shape an OSS contribution story.
---

# Contribute Open Source Agent

## Core Posture

Drive the contribution end to end, but keep scope small enough that maintainers can review it. Prefer one focused PR that improves a concrete agent behavior over a broad refactor or peripheral cleanup.

Use current GitHub data when checking repository activity, issues, pull requests, maintainer responsiveness, and PR collision risk. If network access or GitHub authentication is unavailable, explain the limitation and continue with local repository analysis.

Do not do broad GitHub repository discovery. Analyze only the fixed repository pool unless the user explicitly provides another repository.

Only pursue PRs that change or test the repository's core agent behavior: planning, tool routing and execution, context or memory management, multi-agent orchestration, eval trajectory, safety or human approval gates, failure recovery, or replanning.

Exclude docs-only, UI-only, setup-only, dependency-only, formatting-only, and generic engineering cleanup PRs unless they directly support one of those core agent behaviors.

## Default Repository Pool

Analyze these repositories first, in this order unless the user gives a different priority:

| Repository | Core-agent angle |
|---|---|
| https://github.com/openclaw/openclaw | Agent runtime, gateway, skills, MCP/tool execution, safety gates, workflow continuation. |
| https://github.com/anomalyco/opencode | Coding agent loop, tool execution, permission model, provider/tool routing, session state. |
| https://github.com/MoonshotAI/kimi-code | Terminal coding agent loop, skills, MCP, subagents, hooks, ACP, context handling. |
| https://github.com/NousResearch/hermes-agent | Python agent runtime, tool gateway, provider/tool diagnostics, execution reliability. |
| https://github.com/HKUDS/nanobot | Lightweight agent workflows, tools, memory, chat/task orchestration, execution loop. |
| https://github.com/fastclaw-ai/fastclaw | Multi-agent runtime, orchestration, plugin bridge, tool execution, agent coordination. |

For repository-specific inspection hints, read `references/repository-pool.md`.

## Reference Routing

Read the smallest relevant reference before acting:

- For repository selection and file-entry hints, read `references/repository-pool.md`.
- For deciding whether an opportunity is core-agent work, read `references/core-agent-opportunity-rubric.md`.
- For issue screening, PR collision checks, technical design, implementation guardrails, PR drafting, and interview narration, read `references/pr-workflow.md`.

## Workflow

1. Clarify or infer the user's contribution goal:
   - Core agent area: planning, tool routing/execution, context, memory, multi-agent orchestration, evals, safety gates, recovery, or replanning.
   - Skills to highlight: Python, TypeScript, Go, Node, MCP, evals, testing, architecture, or agent runtime design.
   - Timebox: default to a PR that can be completed in 1-2 weeks.

2. Select candidate repositories from the fixed pool:
   - Do not run broad GitHub discovery.
   - Refresh current GitHub signals for the pool: recent commits, issues, PRs, labels, contribution guide, and maintainer response patterns.
   - Rank the pool by core-agent fit, activity, reviewability, issue quality, contribution rules, and interview value.
   - Down-rank repositories where core-agent issues are stale, PRs sit unreviewed for months, or contribution rules are unclear.

3. Select core-agent contribution opportunities:
   - First screen open issues, but keep only issues that affect core agent behavior.
   - Prefer active, unassigned issues with clear expected behavior, reproducible steps, or concrete acceptance criteria.
   - Before recommending an issue, verify it has no linked or in-progress PR.
   - If issues are thin, inspect core agent modules for small gaps that can be fixed or tested in 1-3 files.
   - Exclude peripheral work even if it is easy.

4. Build project understanding before proposing work:
   - Read `README.md`, `CONTRIBUTING.md`, package/test config, and likely core agent entry files.
   - Summarize the core agent loop, planning style, tool layer, state/memory model, eval/test setup, and safety or approval model.
   - Run the documented quickstart or existing tests if feasible.

5. Choose a PR direction:
   - Rank the top 1-3 options by core-agent impact, maintainer acceptance chance, implementation size, testability, and interview value.
   - For nontrivial behavior changes, draft a concise issue or discussion comment before coding and ask whether maintainers want that direction.
   - Do not proceed with a large feature, new dependency, public API change, or broad redesign without maintainer signal or explicit user approval.

6. Design before editing:
   - Define the core agent behavior being changed or tested, out-of-scope items, success criteria, constraints, and changed files.
   - Compare 2-3 implementation options when the design is not obvious.
   - Keep the recommended plan backward compatible and preferably under about 300 changed lines for a first PR.

7. Implement conservatively:
   - Read every file that will be changed before editing.
   - Match naming, types, comments, formatting, and test style already present.
   - Prefer extension points over invasive rewrites.
   - Keep each step runnable and verify after meaningful changes.
   - Stop and ask the user if scope expands beyond core-agent work, compatibility cannot be preserved, a new dependency is needed, or two viable designs need a product judgment.

8. Prepare the PR:
   - Draft a PR with Problem, Solution, Changes, Testing, and Notes for Reviewer.
   - Include exact test commands and outcomes.
   - If actually opening the PR requires authentication or network access, request permission and report the URL or remaining manual step.

9. Preserve interview evidence:
   - Capture the repository context, core-agent behavior changed, files touched, tests, tradeoffs, maintainer feedback, and final PR status.

## Output Shapes

For repository ranking, return a table with repository, core-agent fit, health signals, likely core modules, likely contribution paths, and risk.

For opportunity analysis, return a ranked Top 3 with source, core-agent behavior, entry files, expected effort, PR collision check, acceptance risk, test strategy, and interview value.

For implementation tasks, finish with changed files, tests run, remaining risks, and PR draft or PR URL.

For interview prep, produce a concise STAR-style story grounded in the actual PR, files changed, tests, review comments, and measurable impact.