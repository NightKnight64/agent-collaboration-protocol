# Handoff Message Format

Use this template when spawning or messaging agents. Include ALL fields.

```
## Handoff: {Title}

**What:** {Specific task or deliverable — one sentence}

**Why:** {Context and priority — why this is needed now}

**Build directory:** {Absolute path to shared/build-{YYYYMMDD}/}

**Files:**
- `{ABSOLUTE_BUILD_DIR}/SPEC.md` — API contract
- `{ABSOLUTE_BUILD_DIR}/backend/` — write backend code here
- `{ABSOLUTE_BUILD_DIR}/backend-log.md` — log progress here

**Success criteria:** {Observable behavior — how we know it's done}

**ETA:** {YYYY-MM-DD HH:MM UTC}
```

## Handoff Acknowledgment (MANDATORY)

The receiving agent **must reply with ACK** before starting work:

> "ACK — confirmed build directory: /path/to/shared/build-{YYYYMMDD}/"

This confirms:
1. The agent received the handoff
2. The agent can resolve the build directory path
3. The agent understands the task context

**If no ACK within 2 minutes: re-spawn the agent.** Do not wait indefinitely.

## Monitoring

1. **T+2 min:** Did the agent ACK? If not, re-spawn.
2. **T+5 min:** Did the agent produce its first log entry? Files modified?
3. **Near ETA:** Progress? Blockers?
4. **At ETA:** If no progress and no communication, re-spawn or escalate.

**Don't poll aggressively.** Subagents return results when they finish. Check only at these milestones.
