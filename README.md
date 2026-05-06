# Agent Collaboration Protocol

Structured multi-agent collaboration for backend + frontend builds.

## Overview

Three roles collaborate through a shared workspace:

| Role | Responsibility |
|------|---------------|
| **Orchestrator** | Defines the contract, spawns both builders, verifies integration, merges |
| **Backend Engineer** | Writes API code, data models, infrastructure |
| **Frontend Engineer** | Writes UI components, templates, styles |

The contract lives in `shared/build-{YYYYMMDD}/`. Each builder writes to its own subdirectory with its own log file — **no conflicts, ever**. The orchestrator inspects and merges when both are done.

## Quick Start

1. Run `scripts/init_collab.sh /path/to/project` to create the shared workspace
2. Edit `shared/SPEC.md` with your feature contract
3. Spawn backend and frontend agents (see SKILL.md for task templates)
4. Both agents build simultaneously, logging to their own files
5. Orchestrator verifies and merges

## What's New in v1.3.0

- **Separate log files** — `backend-log.md` and `frontend-log.md` eliminate race conditions. No more simultaneous-write conflicts.
- **Abort thresholds** — Clear triggers for when to stop debugging the collaboration and re-scope (3 crashes → split task, 2 no-file attempts → rewrite handoff, 15+ min no log → kill and restart).
- **Handoff ACK requirement** — Receiving agents must confirm receipt and path before starting. No ACK in 2 min → re-spawn.
- **Enhanced init script** — Framework stubs (`--framework fastapi|express`), dry-run mode (`--dry-run`), OpenClaw version detection, log file template creation.

### v1.2.0

- **Absolute path requirement** — Orchestrator must provide full absolute paths to subagents
- **Artifact verification step** — "Check that files actually landed" as a required step
- **{ABSOLUTE_BUILD_DIR} convention** — Consistent placeholder in all templates

### v1.1.0

- **Recovery Protocol** — Concrete steps for agent crashes, build mismatches, and blockers
- **Shared Constants** — Status enums, error codes, and feature flags
- **Verification Guide** — Backend curl tests, frontend state checklist, integration checks
- **MIT-0 License** — Simplest possible open source license

## Documentation

- `SKILL.md` — Full workflow, abort thresholds, recovery protocol, verification guide
- `references/spec-template.md` — Complete SPEC.md template with examples
- `references/integration-log.md` — Per-agent log file format + orchestrator merge format
- `references/handoff-format.md` — Task handoff template (includes ACK requirement)

## When Not to Use

- Single-file changes (just do it directly)
- Solo tasks that don't cross backend/frontend boundaries
- Bug fixes that are purely backend or purely frontend
- Tasks where one agent can handle both sides (use a single subagent instead)

## License

MIT-0 — do whatever you want, no attribution required.
