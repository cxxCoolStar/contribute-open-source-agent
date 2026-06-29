---
name: contribute-open-source-agent
description: Find suitable AI Agent open-source repositories, identify high-leverage contribution opportunities, design and implement scoped fixes or features, prepare pull requests, and shape the contribution into interview-ready evidence. Use when the user wants to contribute to open source, find GitHub projects or issues, analyze an AI Agent repository for PR ideas, implement a contribution, draft maintainer communication, submit or prepare a PR, or turn an OSS contribution into an interview story.
---

# Contribute Open Source Agent

## Core Posture

Drive the contribution end to end, but keep scope small enough that maintainers can review it. Prefer one focused PR that solves a clear problem over a broad refactor.

Use current GitHub data when selecting repositories, issues, release cadence, maintainer responsiveness, or PR status. If network access or GitHub authentication is unavailable, explain the limitation and continue with local repository analysis.

When the task involves detailed opportunity scoring, architecture review, PR drafting, maintainer outreach, or interview narration, read `references/contribution-workflow.md`.

## Workflow

1. Clarify or infer the user's contribution goal:
   - Target domain: AI Agent, MCP, LangChain/LlamaIndex, evals, tool routing, orchestration, memory, UI, docs, tests, or bug fixing.
   - Skills to highlight: Python, TypeScript, React, Node, MCP, evals, testing, docs, or architecture.
   - Timebox: default to a PR that can be completed in 1-2 weeks.

2. Find candidate repositories:
   - Search GitHub with queries such as `topic:ai-agent stars:>1000 pushed:>YYYY-MM-DD`.
   - Favor repos with recent commits, active issue triage, healthy closed/open issue ratio, maintainer responses within roughly 2 weeks, and monthly or quarterly releases.
   - Avoid repos where issues are stale, PRs sit unreviewed for months, or contribution rules are unclear.

3. Select contribution opportunities:
   - First check open issues with labels like `good first issue`, `help wanted`, `bug`, `documentation`, `enhancement`, and project-specific equivalents.
   - Prefer open, recently active, unassigned issues with clear expected behavior or reproducible steps.
   - Estimate whether the likely change fits 1-3 files and does not require architecture-wide redesign.
   - If issues are thin, inspect the codebase for small AI Agent architecture gaps.

4. Build project understanding before proposing work:
   - Read `README.md`, `CONTRIBUTING.md`, `CHANGELOG.md` or `HISTORY.md`, package config, test config, and core entry files.
   - Summarize the core Agent loop, planning style, tool layer, state/memory model, eval/test setup, and runtime stack.
   - Run the documented quickstart or existing tests if feasible.

5. Choose a PR direction:
   - Rank the top 1-3 options by user fit, maintainer acceptance chance, implementation size, testability, and interview value.
   - For nontrivial features, draft a concise issue or discussion comment before coding and ask whether maintainers want that direction.
   - Do not proceed with a large feature, new dependency, API change, or broad redesign without maintainer signal or explicit user approval.

6. Design before editing:
   - Define the core problem, out-of-scope items, success criteria, constraints, and changed files.
   - Compare 2-3 implementation options when the design is not obvious.
   - Keep the recommended plan backward compatible and preferably under about 300 changed lines for a first PR.

7. Implement conservatively:
   - Read all files that will be changed before editing.
   - Match naming, types, comments, formatting, and test style already present.
   - Prefer extension points over invasive rewrites.
   - Keep each step runnable; verify after meaningful changes.
   - Stop and ask the user if the required scope expands materially, a new dependency is needed, or two viable designs need a product judgment.

8. Prepare the PR:
   - Create a focused branch when working in a real repo.
   - Split commits by logical unit when the user asks for commits.
   - Draft a PR with Problem, Solution, Changes, Testing, and Notes for Reviewer.
   - Include exact test commands and outcomes.
   - If actually opening the PR requires authentication or network access, request permission and report the URL or remaining manual step.

9. Follow up:
   - Track maintainer review comments and respond with concise rationale or updates.
   - If no response after the user's chosen wait period, draft a polite follow-up.
   - Keep an interview narrative: context, contribution, process, result, difficulties, reflection, and skills demonstrated.

## Output Shapes

For repository search, return a ranked table with repository, why it fits, health signals, likely contribution paths, and risk.

For opportunity analysis, return a ranked Top 3 with source, entry files, expected effort, acceptance risk, test strategy, and interview value.

For implementation tasks, finish with changed files, tests run, remaining risks, and PR draft or PR URL.

For interview prep, produce a concise STAR-style story grounded in the actual PR, files changed, tests, review comments, and measurable impact.