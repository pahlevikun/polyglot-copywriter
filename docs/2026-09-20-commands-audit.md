# Commands audit — polyglot-copywriter

**Date:** 2026-09-20  
**Method:** learn-codebase orientation (SKILL.md → README → commands/ → Clarity parity → mode refs)

## Purpose

`commands/` holds optional slash-command wrappers for Claude Code (and compatible hosts). Each file maps a `/polyglot-*` name to an explicit mode in `SKILL.md`. The skill router still resolves language, register, overlay, and use case from the user prompt; commands only pin the **mode** so users do not have to repeat "interview mode" or "do not rewrite the file."

## Current inventory

| File | Slash name | SKILL.md mode | Aliases covered | Status |
|---|---|---|---|---|
| `polyglot-interview.md` | `/polyglot-interview` | co-write (`interview`) | `write`, `draft`, `new` | Present — quality OK |
| `polyglot-rewrite.md` | `/polyglot-rewrite` | rewrite | `edit`, `fix`, **`humanize`** | Present — quality OK |
| `polyglot-review.md` | `/polyglot-review` | review | `critique`, `check` | Present — quality OK |
| `polyglot-lint.md` | `/polyglot-lint` | lint | `stats` | **Added** (was missing) |

### Gaps found (before this task)

- **lint / stats** — documented in README and SKILL.md but had no slash wrapper.
- README install line listed only three slash names; file tree showed three command files.
- No dedicated `polyglot-humanize.md` — intentional (see below).

## SKILL.md modes not wrapped

| Mode / alias | Wrapped? | Notes |
|---|---|---|
| `interview` / `write` / `draft` / `new` | Yes → `/polyglot-interview` | One wrapper covers all co-write aliases |
| `rewrite` / `edit` / `fix` / `humanize` | Yes → `/polyglot-rewrite` | `humanize` is a rewrite alias, not a separate mode |
| `review` / `critique` / `check` | Yes → `/polyglot-review` | |
| `lint` / `stats` | Yes → `/polyglot-lint` | Self-check only; no file edits |

**No separate `/polyglot-humanize`:** `SKILL.md` routes `humanize` to rewrite and loads `humanize-workflow.md` as part of the rewrite pipeline when the use case or user intent matches. A duplicate wrapper would split traffic for the same mode. Users who want humanize explicitly can say so in the `/polyglot-rewrite` argument or use plain language with the skill installed.

## Parity vs Clarity

Clarity ships three commands only: `/clarity-interview`, `/clarity-rewrite`, `/clarity-review`. Polyglot adds a fourth mode (**lint**) in SKILL.md that Clarity does not expose as a first-class slash command. Recommendation: **keep `/polyglot-lint`** — it matches polyglot's evaluation self-check and README examples ("Lint this email against the skill rubric"). Do not drop lint to match Clarity's three-command set.

Format parity: frontmatter (`description`, `argument-hint`) + body opening `Use the \`polyglot-copywriter\` skill in <mode> mode for/on: $ARGUMENTS` matches Clarity's pattern.

## Polyglot constraints (all command bodies)

Commands should remind the agent of constraints that SKILL.md already enforces:

1. **Language resolves first** — register, overlay, use case before mode-specific work.
2. **Incident / chat / email / docs with facts** → rewrite, never interview (`interview.md` § When to skip).
3. **`[TK: …]`** — missing facts become marked gaps, not invented detail (`substance.md`).
4. **Review / lint** — no replacement draft, no file create/modify unless the user asks separately.
5. **Protected artifacts** — numbers, names, links, commands preserved on rewrite.

## Files edited in this task

| Path | Change |
|---|---|
| `commands/polyglot-lint.md` | New lint/stats wrapper |
| `commands/polyglot-interview.md` | Verify; optional incident-skip reminder |
| `commands/polyglot-rewrite.md` | Verify; optional `[TK:]` reminder |
| `commands/polyglot-review.md` | Verify (no change expected) |
| `README.md` | List all four slash names; update file tree; install line unchanged (`cp commands/*.md`) |
| `docs/2026-09-20-commands-audit.md` | This audit |

Monorepo mirror: `teamharness-main/bundle/skills/builtin/polyglot-copywriter/` — same files synced after standalone commit.

## Test / gotcha

- **`commands/` is optional.** `scripts/validate_skill.py` does not require command files; it checks registry, links, eval cases, and language pack integrity.
- **README is the user-facing inventory.** Every slash wrapper must appear in the dedicated form section and in the repository tree.
- **Install path:** `cp commands/*.md ~/.claude/commands/` — filenames become slash names (no extension).
- **No "Related projects" section** in README — removed earlier; verify absent after edits.
- **Gates (standalone root):**

```bash
python3 scripts/validate_skill.py
python3 -m unittest discover -s tests -q
```
