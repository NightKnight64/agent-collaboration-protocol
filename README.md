# Agent Collaboration Protocol

> Structured multi-agent collaboration for backend + frontend builds.

When your orchestrator needs to coordinate a backend engineer and a frontend engineer on the same feature, this protocol prevents merge-hell before it starts. Three roles. One contract. One shared workspace.

## Quick Start

```bash
clawhub install agent-collaboration-protocol
```

Then, in your project:

```bash
./init_collab.sh /path/to/your/project
```

See [SKILL.md](SKILL.md) for full protocol instructions.

## How It Works

| Role | Responsibility |
|------|---------------|
| **Orchestrator** | Defines API contract, spawns agents, verifies integration |
| **Backend Engineer** | Implements API spec, writes to `shared/build-{date}/backend/` |
| **Frontend Engineer** | Implements UI from spec, writes to `shared/build-{date}/frontend/` |

Both agents build simultaneously from the same contract (`SPEC.md`), tracking progress in `integration.md`. The orchestrator inspects, sends corrections if needed, and merges.

## Contents

```
agent-collaboration-protocol/
├── SKILL.md                 ← Full protocol — what to say to each agent
├── clawhub.json             ← Skill manifest
├── scripts/
│   └── init_collab.sh       ← One-command workspace setup
└── references/
    ├── spec-template.md     ← API contract template
    ├── integration-log.md   ← Progress tracking template
    └── handoff-format.md    ← Task handoff message format
```

## Use Cases

- Building a new API + dashboard from scratch
- Adding a feature requiring backend changes + new UI
- Refactoring a monolith into API + frontend layers
- Any task where two agents need to stay in sync across boundaries

## Installation

### Via ClawHub (recommended)

```bash
clawhub install agent-collaboration-protocol
```

### Via GitHub

```bash
git clone https://github.com/NightKnight64/agent-collaboration-protocol.git
```

## Requirements

- An agent platform with subagent spawning (OpenClaw, Claude Code, Cursor, etc.)
- Access to at least one backend-capable and one frontend-capable model
- Bash (for the setup script)

## License

MIT — see [LICENSE](LICENSE)
