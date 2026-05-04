# Project OS

The operating system for human-agent software development, from planning to deployment.

Project OS is a suite of tools that covers the full lifecycle of building software with AI agents: project setup, planning, task management, pre-flight validation, deployment, and operational monitoring.

## Modules

```
Plan → Build → Validate → Deploy → Monitor
```

| Module | Role | Repo | Live | Status |
|--------|------|------|------|--------|
| **project-forge** | Project scaffolding and bootstrap | [project-forge](https://github.com/LanNguyenSi/project-forge) | [project-forge.opentriologue.ai](https://project-forge.opentriologue.ai) | active |
| **scaffoldkit** | Declarative project scaffolding engine (runtime dep of project-forge) | [scaffoldkit](https://github.com/LanNguyenSi/scaffoldkit) | via project-forge | beta |
| **agent-planforge** | Architecture planning, ADRs, initial backlog | [agent-planforge](https://github.com/LanNguyenSi/agent-planforge) | via project-forge | beta |
| **agent-tasks** | Human-agent task workflow and collaboration | [agent-tasks](https://github.com/LanNguyenSi/agent-tasks) | [agent-tasks.opentriologue.ai](https://agent-tasks.opentriologue.ai) | active |
| **agent-preflight** | Local validation before push or handoff | [agent-preflight](https://github.com/LanNguyenSi/agent-preflight) | | beta |
| **deploy-panel** | Deployment management, rollback, status | [deploy-panel](https://github.com/LanNguyenSi/deploy-panel) | [deploy-panel.opentriologue.ai](https://deploy-panel.opentriologue.ai) | active |
| **agent-relay** | Controlled execution on target servers | [agent-relay](https://github.com/LanNguyenSi/agent-relay) | via deploy-panel | active |
| **harness** | Declarative control plane: one YAML for grounding, tools, memory, hooks, policies | [harness](https://github.com/LanNguyenSi/harness) | | beta |
| **project-pilot** | Unified control plane across modules | [project-pilot](https://github.com/LanNguyenSi/project-pilot) | | alpha |
| **agent-ops-dashboard** | Operational monitoring and agent health | [agent-ops-dashboard](https://github.com/LanNguyenSi/agent-ops-dashboard) | [ops.opentriologue.ai](https://ops.opentriologue.ai) | active |

## How they connect

```
                    ┌──────────────┐
                    │ project-pilot│  ← Control Plane
                    └──────┬───────┘
                           │
    ┌──────────┬───────────┼───────────┬──────────┐
    ▼          ▼           ▼           ▼          ▼
┌────────┐┌──────────┐┌──────────┐┌────────┐┌──────────┐
│project-││  agent-   ││  agent-  ││  agent ││  deploy  │
│ forge  ││planforge  ││  tasks   ││preflight│  panel   │
│        ││          ││          ││        ││          │
│Scaffold││  Plan    ││  Work   ││Validate││ Deploy   │
└────────┘└──────────┘└──────────┘└───┬────┘└────┬─────┘
                                      │          │
                                      ▼          ▼
                                 ┌──────────────────┐
                                 │   agent-relay     │
                                 │ (VPS execution)   │
                                 └────────┬──────────┘
                                          │
                                          ▼
                                 ┌──────────────────┐
                                 │agent-ops-dashboard│
                                 │   (monitoring)    │
                                 └──────────────────┘
```

## Key Features

### Deploy Panel
- Sidebar UI with server health monitoring (CPU/RAM/Disk)
- Deploy API v1 with API key auth for CI/CD
- MCP server for AI agent deployments
- GitHub Action for automated post-merge deploys
- Audit log, bulk deploy, scheduled deploys
- Real-time deploy step streaming via SSE
- Browser notifications on completion

### Agent Tasks
- Kanban board for human-agent task collaboration
- Task lifecycle: open → in_progress → review → done
- PR creation and merge via GitHub delegation
- Task instructions with confidence scoring

### Agent Relay
- Controlled deployments on VPS targets via Docker
- Pre-flight checks, health monitoring, rollback
- Git-based deployment flow with step-by-step execution

## Getting Started

Each module runs independently. Start with what you need:

1. **Just deploying?** → [deploy-panel](https://github.com/LanNguyenSi/deploy-panel) + [agent-relay](https://github.com/LanNguyenSi/agent-relay)
2. **Task management?** → [agent-tasks](https://github.com/LanNguyenSi/agent-tasks)
3. **Full lifecycle?** → Start with project-forge, plan with agent-planforge, work with agent-tasks, validate with agent-preflight, deploy with deploy-panel

## Related Projects

| Project | Description | Live |
|---------|-------------|------|
| [agent-grounding](https://github.com/LanNguyenSi/agent-grounding) | Verification framework: runtime checks, claim validation, hypothesis tracking | |
| [depsight](https://github.com/LanNguyenSi/depsight) | GitHub-connected developer security dashboard: CVE tracking, license compliance, dependency health | [depsight.opentriologue.ai](https://depsight.opentriologue.ai) |
| [codebase-oracle](https://github.com/LanNguyenSi/codebase-oracle) | Local-first MCP server, semantic index over your repos | |
| [agent-memory](https://github.com/LanNguyenSi/agent-memory) | Sync, weave, and digest agent memories across sessions | |
| [telerithm](https://github.com/LanNguyenSi/telerithm) | AI-powered log analytics for self-hosted teams | |
| [triologue](https://opentriologue.ai) | Real-time AI ↔ AI ↔ Human collaboration platform (separate product) | [opentriologue.ai](https://opentriologue.ai) |

## Maturity

We use honest maturity labels:

- **alpha**: functional but API may change significantly
- **beta**: core features stable, edges may be rough
- **active**: in production use, actively developed
- **stable**: battle-tested, breaking changes are rare
