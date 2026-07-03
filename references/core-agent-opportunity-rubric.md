# Core Agent Opportunity Rubric

Use this reference to decide whether a contribution is in scope. A PR is in scope only when it changes, protects, or tests observable agent behavior.

## In-Scope Core Agent Areas

### 1. Agent Loop and Planning

Examples:

- Fix how the agent chooses the next step.
- Add or test replanning after tool failure.
- Preserve task state across continuation or resume.
- Improve termination conditions to avoid premature exit or infinite loops.

Evidence to collect: files/functions that drive the agent loop, state transitions, step execution, and tests or fixtures that can observe the behavior.

### 2. Tool Routing and Execution

Examples:

- Fix tool selection, argument validation, or tool-result handling.
- Reduce confusion between similar tools.
- Add tests for tool-call parameters or failed tool calls.
- Improve MCP/tool adapter behavior without changing broad public APIs.

Evidence to collect: tool schema construction, router logic, execution wrapper, error propagation, permission checks, and trajectory tests.

### 3. Context and Memory

Examples:

- Fix loss of important tool results during compression or trimming.
- Preserve system/developer instructions separately from conversation content.
- Improve memory retrieval only when it changes agent decisions.
- Add tests around token-limit or resume behavior.

Evidence to collect: context builders, compression/summarization logic, memory read/write paths, transcript representation, and boundary tests.

### 4. Multi-Agent Coordination

Examples:

- Fix handoff protocol, role routing, shared state, or aggregation.
- Add tests for worker/orchestrator interactions.
- Improve failure isolation between agents.

Evidence to collect: orchestrator code, role definitions, handoff messages, shared state model, and tests that observe coordination behavior.

### 5. Eval Trajectory and Agent Tests

Examples:

- Add trajectory-level tests for planning/tool behavior.
- Assert tool calls and intermediate decisions, not only final text.
- Add a small fixture that captures a known agent failure.

Evidence to collect: eval harness, test fixtures, fake tools/providers, snapshot format, and CI constraints.

### 6. Safety, Permissions, and Human-in-the-Loop

Examples:

- Fix missing confirmation before high-risk tool use.
- Preserve human feedback across later steps.
- Add tests that rejected operations do not proceed.

Evidence to collect: permission gates, approval prompts, risk classification, human feedback storage, and tests around blocked execution.

### 7. Failure Recovery

Examples:

- Convert tool/provider errors into recoverable agent state.
- Retry, fallback, or replan only where the existing design supports it.
- Improve diagnostic surface when it affects agent execution correctness.

Evidence to collect: error handling paths, retry policy, recovery state, and tests for failed tool/provider calls.

## Out-of-Scope By Default

Reject or down-rank these unless they directly support one in-scope behavior above:

- Docs-only or translation-only PRs.
- UI-only polish, themes, layout, icons, or copy changes.
- Setup-only, install-only, deployment-only, or packaging-only work.
- Dependency upgrades or lockfile churn.
- Formatting, lint-only, or broad cleanup PRs.
- Generic bug fixes that do not affect agent behavior.
- Large new integrations that add surface area without improving core agent behavior.

## Opportunity Score

Score each candidate from 1-5:

| Dimension | Question |
|---|---|
| Core-agent impact | Does it change or test planning, tools, context, memory, orchestration, evals, safety, or recovery? |
| Reviewability | Can it fit in 1-3 files and avoid public API churn? |
| Testability | Can behavior be verified with unit, integration, or trajectory tests? |
| Ownership fit | Is the issue unassigned and unclaimed, or has outside help been explicitly invited? |
| Maintainer fit | Does it match existing architecture and maintainer priorities? |
| Interview value | Can the contribution demonstrate agent architecture judgment? |

Prefer opportunities with total score 22+ and no score below 3. Exclude assigned or claimed issues unless outside help is explicitly invited. If a candidate is mostly peripheral, exclude it even if it is easy.