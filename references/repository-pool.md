# Fixed Repository Pool

Use this reference to inspect the fixed repository pool. Treat these hints as starting points, not facts; verify against the current repository before recommending work.

## Selection Rules

- Do not search for additional repositories by default.
- Rank repositories by likely core-agent contribution value, not general popularity.
- Prefer repositories where a small PR can change or test observable agent behavior.
- Down-rank repositories whose available work is mostly UI polish, docs, packaging, setup, dependency bumps, or unrelated infrastructure.

## Repository Pool

| Repository | Stack Signal | Core modules to inspect first | Avoid by default |
|---|---|---|---|
| https://github.com/openclaw/openclaw | TypeScript/Node personal assistant and agent runtime | Agent loop, gateway, skills, MCP/tool execution, permission/safety gates, workflow continuation, tests around tool calls | UI polish, extension marketplace metadata, docs-only changes |
| https://github.com/anomalyco/opencode | TypeScript coding agent | Session/agent loop, tool execution, provider routing, permission model, context handling, tests around command/tool behavior | TUI cosmetics, theme work, generic CLI docs |
| https://github.com/MoonshotAI/kimi-code | TypeScript/Vue terminal coding agent | Agent loop, skills, MCP, subagents, hooks, ACP, context management, execution state | Vue-only UI work, branding/docs-only tasks |
| https://github.com/NousResearch/hermes-agent | Python personal agent | Agent runtime, tool gateway, provider/tool diagnostics, execution errors, tests around agent/tool behavior | Setup-only fixes, provider docs-only changes |
| https://github.com/HKUDS/nanobot | Python/TypeScript lightweight agent | Workflow execution, tools, memory, chat/task orchestration, agent state, deployment paths only when they affect execution | Frontend polish, deployment docs-only changes |
| https://github.com/fastclaw-ai/fastclaw | Go/TypeScript multi-agent framework | Multi-agent runtime, orchestration, plugin bridge, tool execution, agent coordination, tests around agent handoff | Control-plane UI polish, marketing/docs-only tasks |

## Ranking Output

When ranking repositories, use this table:

| Rank | Repository | Core-Agent Fit | Fresh Health Signals | Likely Entry Files | Best PR Direction | Risk |
|---|---|---|---|---|---|

Core-Agent Fit should explain the agent behavior that can plausibly be changed or tested, not just the repository's general domain.