# Maestro — Example

Self-contained run: only `/maestro` required. See [phases.md](phases.md) for templates.

## Phase 0

```
MAESTRO_SCOPE:
TARGET: js/community/chat.js, firestore.rules
TRACK: release
RUNTIME: browser JS + Firestore
TRUST_BOUNDARIES: Firebase Auth; rules enforce writes
OUT_OF_SCOPE: graph engine
AUDIT_MODE: full
```

## Phase index (filled after run)

| Phase | Module | Status | Count |
|-------|--------|--------|-------|
| 0.5 | systematic-debugging | Iron Law | — |
| 1 | security | done | 1 |
| 2 | logical | done | 1 |
| 3 | code quality | done | 1 |
| 4a | frontend | done | 1 |
| 4b | database | skipped | — |
| 4c | python | skipped | — |
| 5 | o1-performance | done | 1 |
| 6 | memory-leak | done | 1 |
| 7 | deslop | skipped | no diff |
| 8c | verify-this | VERIFIED | 1 |
| 9 | synthesis | done | — |

## Phase 9 excerpt

**Verdict: Not ready.** Fix `P1-VULN-1`, `P6-LEAK-1`, then `P2-LOG-1`.

| ID | Phase | Summary |
|----|-------|---------|
| P1-VULN-1 | 1 | Open channel writes |
| P2-LOG-1 | 2 | No rollback on failed write |
| P6-LEAK-1 | 6 | onSnapshot not disposed |

Fix order: P1 → P6 → P2 → P4a → P5 → P3.
