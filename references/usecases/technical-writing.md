# Technical Writing — Farhan Yuda Pahlevi

Extracted from: Backfill Contract RFC, Intermittent Login Failures Analysis (Lark docs),
ADR for Self-serve Change Phone/Email for Merchant.

---

## Document Structure Template

Farhan's technical docs follow this skeleton regardless of type (RFC, ADR, incident analysis):

```
1. Background          — number first, then problem statement
2. Why this exists     — motivation, not just description
3. What it does NOT cover  — explicit Non-Goals section
4. Goals & Non-Goals   — table or bullet, one per line
5. Technical detail    — decision matrix, call chain, processing criteria
6. Options (if applicable)  — table with Pros/Cons per option
7. Decision            — at the END, not buried in options
8. Rollout plan        — numbered checklist with dry-run first
```

---

## Opening Pattern: Numbers Before Context

State the scale or impact before the background:

> "~2.99 million active GoFood contracts in Curator have `comfee_exclude_mfp` and/or `vat_calculation_type` stuck at `UNSPECIFIED` — a leftover from before the GoFood billing migration."

> "Peak GOID call is 27K RPM"

> "7 Redix restarts between Jul 1 00:17 and Jul 2 10:02 WIB (~34 hours of instability)"

Formula: `[specific count/metric] [entity] [have/are] [problem] — [root cause in one clause]`

---

## Mental Model Analogies (one-liner before multi-paragraph)

Before explaining complex systems, drop a single analogy sentence:
> "Mental model: the runner is the infrastructure, the script is the business logic."
> "Think of it as: every crash re-opened a cold window."

Analogies come BEFORE the technical explanation, not after.

---

## Sequential Criteria with Unicode Ordinals

For ordered decision logic, use ① ② ③ ④ (not bullets, not numbered lists):

```
① comfee = INCLUDE_MFP (GOBER) → call evaluate-rules → if mismatch AND force=true → GOBER_PATCHED
② vat != UNSPECIFIED AND comfee != UNSPECIFIED → NOT_UNSPECIFIED_SKIP
③ package not in Zeus reference → raise ValueError → _errors.csv
④ at least one UNSPECIFIED + package found → PATCH → PATCHED / DRY_RUN
```

---

## Decision Matrices as Tables

Never write conditional logic as prose. Use a table with labeled outcome column:

| Condition | Evaluate rules? | PATCH curator? | Status |
|---|---|---|---|
| GOBER contract, values match | ✅ | ❌ | `GOBER_SKIP` |
| Both fields already set | ❌ | ❌ | `NOT_UNSPECIFIED_SKIP` |
| Package missing from Zeus | ❌ | ❌ | error → `_errors.csv` |
| At least one UNSPECIFIED + package found | ✅ (observational) | ✅ | `PATCHED` / `DRY_RUN` |

---

## Call Chain as Table (not prose paragraphs)

For multi-layer systems, document the call chain as a table:

| Layer | What happens | Outcome |
|---|---|---|
| Hermes Rails | UserInfoConcern#goid_user_info — calls Saudagar::Merchant.find. No retry. | User Object |
| Ruby Client | Checks MerchantCache → if miss, calls saudagar-ro GET /v1/merchant/:id | JSON or nil |
| Saudagar-ro | Cache.fetch_by_id → Redis hit returns immediately, miss calls ES | 200 or 4xx/5xx |

---

## Goals + Non-Goals (always explicit)

Never leave scope implicit. Always add a Non-Goals section:

```markdown
#### Goals
- Backfill X on all eligible records
- Skip already-set values (idempotent, no double-write)
- Support resume after interruption via checkpoint

#### Non-Goals
- Touching payment_settings (out of scope — contracts only)
- Creating or modifying rules
- Special handling for addendum vs. primary
```

---

## Options Table (Pros/Cons per row)

When multiple solutions exist, present them as a structured table:

| Option | Pros | Cons |
|---|---|---|
| A: Drop error, allow nil | Stops login failures for GMA users; removes Saudagar-RO dependency | goresto_id may be nil — harder to debug |
| B: Fallback to Saudagar Master on failure | Eliminates race condition; master is authoritative | Dual dependency in Hermes-readonly |
| C: Use Saudagar Master completely | Single authoritative source; simpler call chain | Hits master on ALL normal traffic, not just failures |

Then **Decision section at the end** — after all options are visible:
> "After the final session, we decided to use Saudagar-Master directly..."

---

## Timing Simulation Format

For batch operations, always show the math:

```
formula: total_rows ÷ contract_rps = hours

| Contract RPS | WS calls/sec (N=1) | Total hours | 24h run |
|---|---|---|---|
| 4 (conservative) | 8 | ~207h | ~9 days |
| 12 | 24 | ~69h | ~3 days |
```

---

## Rollout Plan Format

Always numbered, always starts with dry-run:

```
1. Dry-run on pod (100 rows)
   ├── Verify: logs show "DRY_RUN", no PATCH calls made
   ├── Verify: output CSV shape is correct
   └── Verify: evaluate-rules columns non-empty

2. Dry-run on pod (full dataset)
   └── Confirm: summary.json total matches expected

3. Live run — Phase A (--limit 500000)
   ├── Monitor: error rate in Grafana
   └── Spot-check 5–10 output rows

4. Live run — Phase B (--resume)
```

---

## Root Cause Hierarchy

Never a flat "causes" list. Label explicitly:
> "The intermittent login failures have **two distinct root causes** operating at different layers, and it's important not to conflate them."
> "**Primary Root Cause:** Race Condition in ES"
> "**Secondary Root Cause:** Redis Instability Widened the Exposure Window"
> "Redis instability was a **multiplier**, not the origin."

---

## Conservative-First Recommendation Pattern

Start conservative, name the trigger to ramp:
> "Recommendation: open at **4 RPS** on the first live run... Once the first 10K rows complete cleanly, ramp to **12 RPS**. If Wallstreet starts returning 429s, drop --rps rather than restarting."

---

## Pronoun Use in Technical Docs

Unlike IDP (always "I"), technical docs use "we" for shared team decisions:
- "We decided to use Saudagar-Master directly"
- "We got a report from the ICP team"
- But: "I drafted the ADR" / "I manage the rollout" — personal ownership stays "I"

---

## MR Description Template (Farhan's style)

```markdown
## What
[One sentence: what changed]

## Why
[One sentence: the specific problem this solves, with numbers if available]

## How
[3–5 bullets: concrete technical changes]
- Added X to Y
- Removed Z (was causing [specific issue])
- Coordinate with [team] for [specific thing]

## Risk
[One line: rollback plan or "no behavioral change to existing flow"]
```

---

## ADR Structure

| Field | Farhan's pattern |
|---|---|
| Status | ACCEPTED / PROPOSED (in code block) |
| Date | YYYY-MM-DD |
| DARCI | Always fills Accountable + Responsible at minimum |
| Context | Numbered scale metric first, then problem description |
| Options | Table with Pros/Cons, or numbered list with tradeoffs |
| Decision | Separate section at the end; plain statement + brief justification |
| Consequences | What changes operationally; what's now true |
