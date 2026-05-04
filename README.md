# Agent Collaboration Protocol

Structured multi-agent collaboration for backend + frontend builds.

## Overview

Three roles collaborate through a shared workspace:

| Role | Responsibility |
|------|---------------|
| **Orchestrator** | Defines the contract, spawns both builders, verifies integration, merges |
| **Backend Engineer** | Writes API code, data models, infrastructure |
| **Frontend Engineer** | Writes UI components, templates, styles |

The contract lives in `shared/build-{YYYYMMDD}/`. Both builders write to the same directory. The orchestrator inspects and merges when both are done.

## Quick Start

1. Run `scripts/init_collab.sh /path/to/project` to create the shared workspace
2. Edit `shared/SPEC.md` with your feature contract
3. Spawn backend and frontend agents (see SKILL.md for task templates)
4. Both agents build simultaneously, updating `integration.md`
5. Orchestrator verifies and merges

## What's New in v1.1.0

- **Recovery Protocol** — Concrete steps for agent crashes, build mismatches, and blockers
- **Shared Constants** — Status enums, error codes, and feature flags that both sides must agree on
- **Verification Guide** — Backend curl commands, frontend state checklist, integration checks
- **Per-Agent Log Format** — Solves simultaneous-write conflicts in integration.md
- **MIT-0 License** — Simplest possible open source license

## Documentation

- `SKILL.md` — Full workflow, recovery protocol, and verification guide
- `references/spec-template.md` — Complete SPEC.md template with examples
- `references/integration-log.md` — Integration log format (standard + per-agent)
- `references/handoff-format.md` — Task handoff message template

## When Not to Use

- Single-file changes (just do it directly)
- Solo tasks that don't cross backend/frontend boundaries
- Bug fixes that are purely backend or purely frontend
- Tasks where one agent can handle both sides (use a single subagent instead)

## License

MIT-0 — do whatever you want, no attribution required.