# Architecture

## Design Principles

1. **Modules, not monolith** — Each tool runs independently. Compose what you need.
2. **Human in the loop** — Agents propose, humans approve. No fully autonomous actions without consent.
3. **Observable by default** — Every action is logged, every state is queryable.
4. **Relay pattern** — Sensitive operations (deployment, server access) go through controlled relay points, never direct agent access.

## Communication Patterns

### Task Flow
```
Human creates task → Agent claims → Agent works → Agent submits PR → Human reviews → Merge → Deploy
```

### Deploy Flow
```
Deploy Panel → Relay → VPS (git pull → build → up → health check)
        ↑                              ↓
    SSE stream ←──── step events ──────┘
```

### Monitoring Flow
```
Agent heartbeats → Ops Gateway → Dashboard
Claude Code hooks → Ops Gateway (PostToolUse = busy, Stop = idle)
```

## Integration Points

| From | To | Method |
|------|----|--------|
| agent-tasks | GitHub | REST API (PR creation, merge) |
| deploy-panel | agent-relay | HTTP + SSE |
| deploy-panel | CI/CD | REST API v1 + GitHub Action |
| deploy-panel | AI agents | MCP server |
| agent-ops-dashboard | agents | Heartbeat REST + SSE |
| claude-code | agent-tasks | Direct API calls |
| claude-code | deploy-panel | MCP tools |
| claude-code | ops-dashboard | Hooks (PostToolUse) |
