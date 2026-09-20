# Anti-slop / humanizer enhancement plan

> **For agentic workers:** Implement P0 then P1. English-only agent instructions. Keep `SKILL.md` ≤ 120 lines. Do not import stop-slop numeric score gates or hillclimb eval infra. Status: **implemented 2026-09-20**.

**Goal:** Selectively import patterns and workflow discipline from [humanizer](https://github.com/blader/humanizer), [anti-slop-writing](https://github.com/adewale/anti-slop-writing), and [stop-slop](https://github.com/hardikpandya/stop-slop) without weakening polyglot's substance layer, multilingual registry, or earned-pattern rule.

**Research basis:** Compared three external skills against bundled `polyglot-copywriter` (2026-09-20). Clarity substance modes were already shipped separately — see [2026-09-20-clarity-substance-modes.md](2026-09-20-clarity-substance-modes.md).

---

## Per-repo summary

### stop-slop

| Dimension | Notes |
|---|---|
| Optimizes for | Surface rhythm, throat-clearing, rhetorical scaffolding |
| Unique imports | Meta-commentary, quotables/pull-quote smell, negative listing |
| Do not copy | Blanket bans (all adverbs, all passive, zero em dashes, all Wh- openers); numeric &lt;35/50 score gate |

### humanizer (v3)

| Dimension | Notes |
|---|---|
| Optimizes for | Surface tells + no-invention guardrails |
| Unique imports | Pattern strength tiers, arguing-with-no-one, vague association, knowledge-limit disclaimers, copula displacement (context-aware), survivor tells, show-work output |
| Do not copy | English-only scope; absolute em-dash ban; duplicate 40-pattern list without dedup map |

### anti-slop-writing

| Dimension | Notes |
|---|---|
| Optimizes for | Substance + mechanism + flow first |
| Unique imports | flow-by-relation, earned/compressed/decorative antithesis, rewrite self-check, adversarial false-positive evals, time-dated vocabulary note |
| Do not copy | Full hillclimb/bootstrap/holdout pipeline inside installable skill |

---

## Gap analysis

### Already strong in polyglot

- Substance before surface (`substance.md`, `[TK:]`, provenance)
- Multilingual registry + honesty for umbrella/limited packs
- Mode contract (interview / rewrite / review / lint)
- Cluster-not-veto + em-dash budget
- Humanize detect → rewrite → verify
- Factual fidelity evals (attribution, docs structure, voice-sample fact leak)

### Conflicts with `substance.md` (do not import)

| Risk | Why |
|---|---|
| Ban all `not X but Y` | Breaks severity distinctions with named mechanism |
| Ban all triads | Breaks operational checklists |
| Ban all adverbs / passive / Wh- openers | Breaks academic hedges, docs, legitimate questions |
| Zero em dashes | Fights voice sample + Pattern 2 aside job |
| Invent mechanism in rewrite | Fights `[TK:]` safeguards |
| Detector score as gate | Forbidden in `substance.md` / `review-prose.md` |

---

## P0 — implemented

| # | Action | Target |
|---|--------|--------|
| 1 | Missing pattern rows (arguing-with-no-one, vague association, knowledge-limit disclaimers, meta-commentary, one-line closers, copula displacement, writing-about-previous-version, quotables) | `references/anti-slop-prose.md` |
| 2 | Pattern strength tiers + emphasis-source test | `references/anti-slop-prose.md` |
| 3 | Survivor tells + rewrite self-check + optional show-work | `references/techniques/humanize-workflow.md` |
| 4 | `Rewrite check:` + optional `Remembered line:` | `references/review-prose.md` |
| 5 | Seven adversarial / false-positive eval cases | `evals/cases.json`, `validate_skill.py`, `test_eval_cases.py` |
| 6 | Related projects (anti-slop-writing, differentiated links) | `README.md` |
| 7 | Development step → flow hinges cross-link | `references/substance.md` |
| 8 | Time-dated vocabulary footer | `references/anti-slop-prose.md` |

---

## P1 — implemented

| # | Action | Target |
|---|--------|--------|
| 9 | `flow-by-relation.md` (relations, hinges, carrier-bound endings, staccato contrast) | `references/techniques/flow-by-relation.md` |
| 10 | Register in technique index + core routing | `techniques/index.json`, `core.md`, `techniques/README.md` |
| 11 | Humanizer ↔ english-humanizer dedup map | `references/usecases/english-humanizer.md` |
| 12 | Show-work note in humanize pack | `references/usecases/humanize/pack.md` |
| 13 | `category: false_positive` partition docs | `CONTRIBUTING.md` |
| 14 | Graded dimensions note (human review only) | `references/evaluation.md` |

---

## Explicitly deferred

| Item | Reason |
|---|---|
| stop-slop numeric &lt;35/50 gate as doctrine | Presentation-only bands already in `evaluation.md`; ablation showed harm as hard gate |
| stop-slop cut-quotables as standalone rule | Folded into emphasis-source test + ending guidance |
| Full anti-slop hillclimb / bootstrap / holdout pipeline | YAGNI for installable skill boundary |
| `evals/adversarial.json` split file | Cases live in `cases.json` with `category: false_positive` |
| `graded_dimensions` in `evaluate_output.py` CI | Documentation-only in `evaluation.md` per plan |
| `prose_stats.py` | Out of scope (YAGNI) |

---

## Verification gates

```bash
cd polyglot-copywriter
python3 scripts/validate_skill.py
python3 -m unittest discover -s tests -q
wc -l SKILL.md   # must be <= 120
```

---

## Atomic commit map (standalone push)

1. `feat(anti-slop): add humanizer and anti-slop-writing patterns`
2. `feat(techniques): add flow-by-relation and staccato contrast`
3. `test(eval): add adversarial false-positive cases`
4. `docs: add anti-slop enhancement plan and README related projects`
5. `docs: publish Clarity-style README essay` (if README essay not already on main)

Sync identical changes to `teamharness-main/bundle/skills/builtin/polyglot-copywriter`; push standalone only.
