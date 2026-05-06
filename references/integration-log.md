# Integration Logs — `shared/build-{YYYYMMDD}/`

## Per-Agent Log Files (default — avoids conflicts)

Each agent writes to its own log file. **No simultaneous-write conflicts possible.**

```
shared/build-{YYYYMMDD}/
  backend-log.md    ← Backend Engineer writes here
  frontend-log.md   ← Frontend Engineer writes here
  integration.md    ← Orchestrator merges findings here
```

### backend-log.md Format

```markdown
# Backend Build Log — {Feature Name}

Started: YYYY-MM-DD HH:MM UTC

## Progress
- HH:MM — Task started
- HH:MM — Router scaffolded at `backend/router.py`
- HH:MM — Models defined at `backend/models.py`
- HH:MM — Endpoint `GET /api/v1/{resource}` responding with mock data
- HH:MM — Shared constants file created
- HH:MM — All endpoints complete, ready for integration testing

## Blockers
- HH:MM — BLOCKER: Need {dependency}. Resolution: {approach or "waiting on orchestrator"}

## Notes
- Any observations about the spec or approach
```

### frontend-log.md Format

```markdown
# Frontend Build Log — {Feature Name}

Started: YYYY-MM-DD HH:MM UTC

## Progress
- HH:MM — Task started
- HH:MM — Component scaffolds created in `frontend/components/`
- HH:MM — API client wired to endpoints from SPEC.md
- HH:MM — Loading/empty/error states handled
- HH:MM — All components complete, ready for integration testing

## Blockers
- HH:MM — BLOCKER: Waiting for backend endpoint `POST /api/v1/{resource}`. Using mock data in meantime.

## Notes
- Any observations about the spec or approach
```

### integration.md (Orchestrator's Merge)

```markdown
# Integration Report — {Feature Name}

## Status
Backend: ✅ Done / ❌ Blocked / ⚠️ Partial
Frontend: ✅ Done / ❌ Blocked / ⚠️ Partial

## Backend Summary
(from backend-log.md)

## Frontend Summary
(from frontend-log.md)

## Integration Issues Found
- Issue: {description} — Resolution: {how fixed or "pending"}
- Issue: {description} — Resolution: {how fixed or "pending"}

## Verification
- [ ] Backend endpoints respond per spec
- [ ] Frontend renders all states correctly
- [ ] API shapes match between frontend and backend
- [ ] Auth flow works end-to-end
- [ ] Shared constants are consistent

## Decision
✅ Merge to production / ❌ Re-spawn {which} agent / ⚠️ Manual intervention needed
```

## Deprecated: Single-File Format

The previous approach used a single `integration.md` for all agents. This caused race conditions when both agents wrote simultaneously. **Do not use.** Migrate existing builds by splitting into backend-log.md and frontend-log.md.
