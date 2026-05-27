---
name: maestro
description: >-
  Self-contained release-audit orchestrator: one skill bundling systematic
  debugging, security, logic, code quality, domain analyzers, performance,
  leaks, deslop, and verification. Use for maestro, full audit, or pre-ship
  review. No separate analyzer skills required.
disable-model-invocation: true
---

# Maestro

**One skill. Full pipeline.** All analyzer methodologies live in [phases.md](phases.md). Execute phases **in table order** — never skip ahead.

## When to use

| Track | Trigger |
|-------|---------|
| **Release** | Pre-ship / pre-merge; "maestro"; "full audit" |
| **Incident** | Specific bug, test failure, regression (`TRACK: incident`) |
| **Quick** | `AUDIT_MODE: quick` — phases marked Quick in table |

## Iron Law (all tracks)

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

Every remediation in Phase 9 must link a **finding ID** → **root cause** → **fix**. See [phases.md § Phase 0.5](phases.md#phase-05--systematic-debugging).

---

## Master phase table

| Phase | Module | Purpose | Run when | Full | Quick | Incident | Finding IDs | Primary output |
|-------|--------|---------|----------|:----:|:-----:|:--------:|-------------|----------------|
| **0** | Maestro scope | Bound target, runtime, trust boundaries, mode | Always | ✓ | ✓ | ✓ | — | `MAESTRO_SCOPE` |
| **0.5** | Systematic debugging | Root cause before fixes; incident investigation | Always (full 4-phase if incident) | ✓ | Iron Law | ✓ full | `P0.5-RC-n` | Root cause report / Iron Law compliance |
| **1** | Security analyzer | Vulns: input, authn, authz, data protection | Always | ✓ | ✓ | ✓* | `P1-VULN-n` | `VULNERABILITY #n` |
| **2** | Logical debugger | Flow, state, edges, error paths | Always | ✓ | ✓ | ✓* | `P2-LOG/STATE/GAP-n` | Logical + State + Gap blocks |
| **3** | Code quality review | Maintainability, 1k-line rule, structure | Full release | ✓ | — | optional | `P3-QA-n` | Quality findings + judo moves |
| **4a** | Frontend debug | DOM, a11y, browsers, mobile | HTML/CSS/JS UI in scope | ✓ | — | if UI | `P4a-FE-n` | `ISSUE #n` (UI/Perf/Compat) |
| **4b** | Database optimizer | SQL, indexes, query plans | SQL/DB/Firestore queries in scope | ✓ | — | if DB | `P4b-DB-n` | `OPTIMIZATION #n` |
| **4c** | Python analyzer | Pythonic patterns, memory, stdlib | `.py` in scope | ✓ | — | if Py | `P4c-PY/OPT-n` | `PATTERN` + `OPTIMIZATION` |
| **5** | O(1) performance | Big-O, bottlenecks, hot paths | Always (release/quick) | ✓ | ✓ | ✓* | `P5-OPT/BOTTLENECK-n` | Performance + roadmap |
| **6** | Memory leak detective | Listeners, DOM, subscriptions, heap growth | Long-lived / session code | ✓ | — | if repro | `P6-LEAK-n` | `LEAK #n` |
| **7** | Deslop | Remove AI slop on branch diff | Git diff vs main available | ✓ | — | — | `P7-SLOP-n` | Minimal slop report |
| **8a** | Compiler check | Compile / typecheck clean | Project has build command | ✓ | — | — | `P8a-BUILD-n` | Error summary |
| **8b** | Smoke tests | E2E smoke pass | `smoketest` or equivalent | ✓ | — | — | `P8b-TEST-n` | Test results |
| **8c** | Verify-this | Prove Critical/High claims | Falsifiable claim exists | ✓ | — | ✓ | `P8c-VERIFY-n` | VERIFIED / NOT VERIFIED / INCONCLUSIVE |
| **8d** | Control UI | Browser repro, screenshots, a11y | UI in scope | ✓ | — | if UI bug | `P8d-UI-n` | Screenshots / traces |
| **9** | Maestro synthesis | Executive report + ship verdict | Always | ✓ | ✓ | ✓ | — | Ship report (below) |

\*Incident track: after Phase 0.5, run only phases relevant to root-cause scope unless user requests full release audit.

### Post-Maestro (not in pipeline order)

| Module | Purpose | When |
|--------|---------|------|
| Review and ship | Commit, PR, ship checklist | After Phase 9, user wants to ship |
| Control CLI | CLI/TUI repro and transcripts | Scope is terminal-only |

### Out of scope for Maestro

Design/generative skills (`frontend-design`, `canvas-design`, `imagegen-*`, `brandkit`, …), PR/CI ops (`fix-ci`, `new-branch-and-pr`, …), reporting (`weekly-review`, `workflow-from-chats`). Use those outside Maestro.

---

## Phase 0 — Scope template

```
MAESTRO_SCOPE:
TARGET: [paths | feature | PR]
TRACK: [release | incident]
RUNTIME: [browser JS | Node | Python | SQL | mixed]
TRUST_BOUNDARIES: [client | API | DB rules | hosting]
OUT_OF_SCOPE: [exclusions]
AUDIT_MODE: [full | quick]
KNOWN_ISSUE: [incident — symptoms, repro, expected vs actual]
```

---

## Execution flow

```text
0 → 0.5 → 1 → 2 → 3 → 4a? → 4b? → 4c? → 5 → 6? → 7? → 8a?→8b?→8c?→8d? → 9
```

**Dependency rule:** Security & logic before structure; structure before domain; domain before algorithmic perf; perf before leaks; analysis before deslop; deslop before verify; verify before synthesis.

For each phase: open [phases.md](phases.md), find `## Phase N`, follow templates **verbatim**.

---

## Phase 9 — Synthesis template

```markdown
# Maestro Audit — [TARGET]

## Executive summary
**Verdict:** Ready | Not ready | Ready with accepted risks
[2–4 sentences]

## Scope
[MAESTRO_SCOPE]

## Incident root cause
[Phase 0.5 summary or N/A]

## Findings by severity
### Critical / High / Medium / Low
- [ID] [Phase] summary → location

## Cross-cutting themes

## Recommended fix order
1. …

## Verification results
| ID | Claim | Verdict | Evidence |

## Phase index
| Phase | Module | Status | Count |

## Ship checklist
- [ ] No open Critical P1/P2
- [ ] Phase 8 run for falsifiable Critical/High items
- [ ] Every fix links finding ID → root cause
```

---

## Publishing

Distribute **only** the `maestro/` folder (`SKILL.md` + `phases.md` + `examples.md`). No other skills required.

---

## Additional resources

- All phase methodologies: [phases.md](phases.md)
- Walkthrough: [examples.md](examples.md)
