# Maestro — Phase methodologies

Execute sections in SKILL.md table order. Use templates verbatim.

---

## Phase 0.5 — Systematic debugging

You apply root-cause discipline before and during all fixes.

### Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

### Four phases (incident track — run fully)

**Phase 1 — Root cause investigation:** Read errors completely; reproduce consistently; check recent changes; gather evidence at component boundaries; trace data flow to source (not symptom).

**Phase 2 — Pattern analysis:** Find working examples in codebase; compare line-by-line; list all differences; map dependencies.

**Phase 3 — Hypothesis:** One hypothesis; smallest test; verify or replace hypothesis — do not stack fixes.

**Phase 4 — Implementation:** Failing test first; single fix; verify; if 3+ fixes failed → question architecture with human partner.

### Release track

Apply Iron Law to every Phase 9 remediation. Map each fix: `finding ID → root cause → change`.

### Output (incident)

```
P0.5-RC-[n]:
SYMPTOM: [...]
ROOT_CAUSE: [...]
EVIDENCE: [...]
FIX_DIRECTION: [...] (implementation in later phases)
```

---

## Phase 1 — Security analyzer

You are a security expert specializing in identifying and fixing security vulnerabilities.

### Layer 1: Vulnerability Scanning

```
SECURITY_AUDIT:
SCOPE:
- Input validation
- Authentication
- Authorization
- Data protection
FINDINGS:
- Vulnerability type
- Risk level
- Attack vectors
```

### Layer 2: Mitigation Strategy

```
MITIGATION_PLAN:
VULNERABILITY:
- Description
- Impact
- Exploitation difficulty
SOLUTION:
- Code changes
- Security controls
- Validation steps
```

### Output

```
VULNERABILITY #[n]:
TYPE: [Category]
SEVERITY: [Critical/High/Medium/Low]
DESCRIPTION:
- Attack scenario
- Potential impact
- Current protection
REMEDIATION:
- Code fixes
- Security measures
- Testing approach
```

**TYPE:** Injection, XSS, CSRF, AuthN, AuthZ, Secrets, Crypto, Config, Dependencies, Logging/PII, DoS, Other.

---

## Phase 2 — Logical debugger

You are a precise logical analyzer specializing in finding subtle bugs and edge cases. Use systematic reasoning to examine code through multiple analytical layers.

### Layer 1: Logical Flow Analysis

```
PATH: [Description]
PRECONDITIONS: [Required states]
STEPS:
1. [Operation 1]
   - Assumptions: [List]
   - Possible Issues: [List]
2. [Operation 2]
POSTCONDITIONS: [Expected states]
INVARIANTS: [Must maintain]
```

### Layer 2: State Management

```
OPERATION: [Name]
CURRENT_STATE: [Before]
MODIFICATIONS:
- Change 1: [What/Why]
- Change 2: [What/Why]
EXPECTED_STATE: [After]
VALIDATION:
- Check 1: [What to verify]
- Check 2: [What to verify]
```

### Layer 3: Edge Case Analysis

```
COMPONENT: [Name]
EDGE_CASES:
1. [Scenario 1]
   - Input: [Example]
   - Current Behavior: [What happens]
   - Correct Behavior: [What should happen]
   - Fix: [Implementation]
2. [Scenario 2]
   ...
```

### Layer 4: Error Propagation

```
ERROR_SCENARIO: [Description]
PROPAGATION:
1. [Origin point]
2. [Intermediate handling]
3. [Final resolution]
CURRENT_HANDLING: [Code]
IMPROVED_HANDLING: [Code]
```

### Output — all three sections

```
ISSUE #[n]:
TYPE: [Category]
SEVERITY: [Critical/High/Medium]
DESCRIPTION: [Clear explanation]
PROOF:
- Precondition: [State]
- Operation: [What happens]
- Result: [Why incorrect]
SOLUTION:
- Fix: [Code]
- Verification: [How to test]
```

```
STATE_ISSUE #[n]:
COMPONENT: [Name]
SCENARIO: [When it occurs]
CURRENT_BEHAVIOR:
- State Changes: [List]
- Problems: [What breaks]
CORRECTION:
- Required Changes: [List]
- Implementation: [Code]
```

```
GAP #[n]:
MISSING: [What's needed]
IMPACT: [Why important]
IMPLEMENTATION:
- Requirements: [List]
- Solution: [Code]
- Tests: [Verification]
```

### Iteration requirements

1. First Pass: Identify logical flows
2. Second Pass: Find state issues
3. Third Pass: Discover edge cases
4. Fourth Pass: Trace error handling
5. Final Pass: Verify solutions

Remember to: show reasoning chain; provide counterexamples; include test cases; consider side effects; document assumptions.

---

## Phase 3 — Code quality review

Extremely strict maintainability review. Push for **code judo** — restructurings that delete complexity, not just move it.

### Non-negotiable standards

0. **Ambitious simplification** — prefer paths that remove branches, helpers, or layers entirely.
1. **1k-line rule** — do not grow a file from under 1k to over 1k without strong reason; extract modules first.
2. **No spaghetti growth** — no ad-hoc conditionals scattered in unrelated flows; use dedicated abstractions.
3. **Clean design over “it works”** — same behavior, better structure.
4. **Boring over magical** — flag brittle generics, pass-through wrappers, hidden assumptions.
5. **Type/boundary cleanliness** — explicit contracts over `any`/silent fallbacks.

### Output

```
P3-QA-[n]:
LOCATION: [file:line or module]
SMELL: [1k-line | spaghetti | abstraction | magic | boundary]
SEVERITY: [High/Medium/Low]
JUDO_MOVE: [restructuring that removes complexity]
IMPLEMENTATION: [sketch or steps]
```

---

## Phase 4a — Frontend debug assistant

You are an expert frontend debugger specializing in UI/UX issues, browser compatibility, and performance optimization.

### Layer 1: DOM Structure Analysis

```
COMPONENT_AUDIT:
STRUCTURE:
- Element hierarchy
- Accessibility issues
- Performance bottlenecks
OPTIMIZATION:
- DOM simplification
- Event delegation
- Resource loading
```

### Layer 2: Browser Compatibility

```
COMPATIBILITY_CHECK:
BROWSERS:
- Chrome/Firefox/Safari versions
- Mobile responsiveness
- Feature detection
FIXES:
- Polyfills needed
- Fallback implementations
```

### Output

```
ISSUE #[n]:
TYPE: [UI/Performance/Compatibility]
SEVERITY: [High/Medium/Low]
REPRODUCTION:
- Steps to reproduce
- Expected behavior
- Actual behavior
SOLUTION:
- Code changes
- Browser-specific fixes
- Performance impact
```

---

## Phase 4b — Database query optimizer

You are a database performance expert focusing on query optimization and index management.

### Layer 1: Query Analysis

```
QUERY_AUDIT: CURRENT:
    SQL structure
    Table access patterns
    Join complexity
OPTIMIZATION:
    Index usage
    Join optimization
    Subquery elimination
```

### Layer 2: Index Strategy

```
INDEX_ANALYSIS: CURRENT:
    Existing indexes
    Usage patterns
    Storage impact
RECOMMENDATIONS:
    New indexes
    Index modifications
    Coverage analysis
```

### Output

```
OPTIMIZATION #[n]:
QUERY: [Original SQL]
ISSUES:
    Performance bottlenecks
    Missing indexes
    Suboptimal joins
SOLUTION:
    Optimized query
    Index changes
    Expected improvement
```

---

## Phase 4c — Python-specific analyzer

You are a Python optimization expert focusing on language-specific patterns and performance.

### Layer 1: Pythonic Pattern Analysis

```
PATTERN_CHECK: CURRENT:
    Implementation: [Code]
    Style: [Assessment]
OPTIMIZATION:
    Pythonic approach: [Better pattern]
    Performance gain: [Expected]
```

### Layer 2: Memory Management

```
MEMORY_AUDIT: COMPONENT: [Name]
CURRENT:
    Allocation: [Pattern]
    Cleanup: [Method]
OPTIMIZATION:
    Memory reduction: [Strategy]
    Resource management: [Approach]
```

### Layer 3: Standard Library Usage

```
STDLIB_ANALYSIS: CURRENT:
    Imports: [List]
    Usage: [Patterns]
OPTIMIZATION:
    Better alternatives: [List]
    Implementation: [Code]
```

### Output

```
PATTERN #[n]:
CURRENT: [Code]
ISSUE: [Why suboptimal]
PYTHONIC_SOLUTION:
    Approach: [Description]
    Code: [Implementation]
    Benefits: [List]
```

```
OPTIMIZATION #[n]:
TARGET: [Component]
CURRENT_PERFORMANCE: [Metrics]
IMPROVEMENT:
    Strategy: [Approach]
    Implementation: [Code]
    Validation: [Tests]
```

---

## Phase 5 — O(1) performance analyzer

You are an expert performance engineer specializing in O(1) optimizations. Your task is to systematically analyze code through multiple iterations of deep reasoning.

### Analysis phases

**Phase 1: Component Identification** — function, operations, data structures, dependencies.

**Phase 2: Complexity Analysis**

```
OPERATION: [Name]
CURRENT_COMPLEXITY: [Big O notation]
BREAKDOWN:
- Step 1: [Operation] -> O(?)
- Step 2: [Operation] -> O(?)
BOTTLENECK: [Slowest part]
REASONING: [Detailed explanation]
```

**Phase 3: Optimization Opportunities**

```
COMPONENT: [Name]
CURRENT_APPROACH:
- Implementation: [Current code]
- Complexity: [Current Big O]
- Limitations: [Why not O(1)]

OPTIMIZATION_PATH:
1. [First improvement]
   - Change: [What to modify]
   - Impact: [Complexity change]
   - Code: [Implementation]
2. [Second improvement]
   ...
```

**Phase 4: System-Wide Impact** — memory, cache, resources, scalability, maintenance.

### Output — all three sections

```
COMPONENT: [Name]
ORIGINAL_COMPLEXITY: [Big O]
OPTIMIZED_COMPLEXITY: O(1)
PROOF:
- Step 1: [Reasoning]
- Step 2: [Reasoning]
...
IMPLEMENTATION:
[Code block]
```

```
BOTTLENECK #[n]:
LOCATION: [Where]
IMPACT: [Performance cost]
SOLUTION: [O(1) approach]
CODE: [Implementation]
VERIFICATION: [How to prove O(1)]
```

```
STAGE 1:
- Changes: [What to modify]
- Expected Impact: [Improvement]
- Implementation: [Code]
- Verification: [Tests]

STAGE 2:
...
```

### Iteration requirements

1. First Pass: Identify all operations above O(1)
2. Second Pass: Analyze each for optimization potential
3. Third Pass: Design O(1) solutions
4. Fourth Pass: Verify optimizations maintain correctness
5. Final Pass: Document tradeoffs and implementation details

Remember to: show all reasoning steps; provide concrete examples; include performance proofs; consider edge cases; document assumptions.

---

## Phase 6 — Memory leak detective

You are a memory management expert specializing in identifying and fixing memory leaks.

### Layer 1: Memory Usage Analysis

```
MEMORY_AUDIT:
PATTERNS:
- Allocation trends
- Reference counting
- Garbage collection
ISSUES:
- Memory growth
- Resource retention
- Cleanup failures
```

### Layer 2: Leak Detection

```
LEAK_ANALYSIS:
SYMPTOMS:
- Growth patterns
- Resource types
- Trigger conditions
DIAGNOSIS:
- Root cause
- Impact assessment
- Prevention strategy
```

### Output

```
LEAK #[n]:
TYPE: [Resource type]
PATTERN:
- Allocation point
- Retention cause
- Growth rate
SOLUTION:
- Code fixes
- Resource management
- Verification steps
```

---

## Phase 7 — Deslop

Remove AI-generated slop from the branch diff vs main.

### Focus

- Unnecessary comments inconsistent with local style
- Abnormal defensive try/catch on trusted paths
- `any` casts to bypass types
- Deep nesting fixable with early returns
- Patterns inconsistent with surrounding code

### Guardrails

- Behavior unchanged unless fixing a clear bug
- Minimal focused edits
- Concise summary (1–3 sentences) plus file list

### Output

```
P7-SLOP-[n]:
FILE: [path]
ISSUE: [slop type]
FIX: [what to remove or rewrite]
```

---

## Phase 8a — Compiler check

1. Run repo compile/typecheck commands.
2. Summarize errors by file and category.
3. Fix highest-confidence issues only if user asked to implement; else report.
4. Re-run until clean or blocked.

### Output

```
P8a-BUILD-[n]:
COMMAND: [...]
STATUS: pass | fail
ERRORS: [grouped summary]
```

---

## Phase 8b — Smoke tests

1. Build prerequisites.
2. Run smoke suite or focused spec.
3. On failure: traces/logs → root cause (link Phase 0.5).
4. Re-run until stable.

### Output

```
P8b-TEST-[n]:
SUITE: [...]
STATUS: pass | fail
FAILURES: [spec, assertion, log snippet]
```

---

## Phase 8c — Verify-this

Prove or disprove falsifiable claims. Return exactly one verdict.

### Workflow

1. Restate claim: condition, metric, threshold.
2. Smallest surface to disprove.
3. Baseline (old/broken state).
4. Treatment (fixed state), same command/environment.
5. Compare artifacts.
6. Verdict: `VERIFIED` | `NOT VERIFIED` | `INCONCLUSIVE`.

### Output

```
P8c-VERIFY-[n]:
VERIFIED | NOT VERIFIED | INCONCLUSIVE
Claim: <falsifiable claim>
Evidence: baseline=..., treatment=..., delta=..., threshold=...
Reasoning: <one paragraph>
```

---

## Phase 8d — Control UI

Browser/CDP harness for UI repro and evidence (screenshots, a11y snapshots, traces).

### Workflow

1. Start app via repo dev command.
2. Reuse existing Playwright/harness if present.
3. Stable selectors: roles, labels, `data-*` — not coordinates.
4. Capture before/after for `verify-this`.

### Output

```
P8d-UI-[n]:
REPRO: [steps]
ARTIFACTS: [screenshot paths, trace refs]
RESULT: [pass | fail vs expected]
```

---

## Post-Maestro — Review and ship

After Phase 9 when user wants to land changes: review diff, run tests, commit/PR per repo conventions. Not a substitute for Phases 1–8.

---

## Post-Maestro — Control CLI

For CLI/TUI scope: repro via terminal harness, capture transcripts for Phase 8c. Use instead of 8d when no browser UI.
