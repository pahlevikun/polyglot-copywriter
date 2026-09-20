# Simple prose (always on)

Global default for **every language**. Read with [core.md](core.md) on every draft. Locale packs choose *which* words and forms fit the register — not *how complicated* the sentence should be.

English and Indonesian examples live in [core.md](core.md). Anti-slop cluster detection stays in [anti-slop-prose.md](anti-slop-prose.md). This file is the **vocabulary and grammar bar** those files assume.

---

## Simple vocabulary

- Prefer words a tired teammate already knows. If you would stop to explain a word, pick a shorter common synonym.
- Avoid Latinate and corporate jargon (`utilize`, `leverage`, `facilitate`, `commence`, `endeavor`, `streamline`, `holistic`) unless the domain, repo, or quoted artifact already uses that exact term.
- One idea per sentence when explaining. Extra facts go in the next sentence.
- Define each acronym once on first use, then use the short form. Never assume the reader knows internal abbreviations.
- Keep technical terms the repo already uses (`repo-natural`, `english-first`, or `indonesia-first` per [core.md](core.md)). Simple prose does not mean dumbing down official names, syntax, or product terms.

## Simple grammar

- Short, complete sentences. If you run out of breath reading aloud, split the line.
- Active voice. Name the actor when known (`We deployed`, `Tim infra`, `I merged`).
- Avoid nested clauses, stacked passives, and connector soup (`furthermore`, `moreover`, `in order to`, `due to the fact that`).
- Match the requested register with the right **forms** (honorifics, pronouns, channel layout) — not with rare words or long sentences.
- Formal (`baku`, legal, academic) still prefers clarity over ornament. Complete sentences ≠ complicated sentences.

## Punctuation

- Default: avoid em dash (`—`) in casual/professional coworker copy; use comma, period, colon, or parentheses.
- Budget: at most one em dash per ~200 words in `santai` / `profesional`; zero preferred in chat and incident updates unless quoting.
- `baku` may use an em dash sparingly for apposition; still prefer splitting into two sentences.
- Cross-language: same restraint in every language — do not copy English em-dash rhythm into other langs.
- Do not chain ideas with em dashes (`fact — explanation — conclusion`); that is an AI rhythm tell. See [anti-slop-prose.md](anti-slop-prose.md).

## Cross-language

These rules apply in **every** registry language — not only English and Indonesian.

- Do not "sound formal" by reaching for rare literary words or multi-clause sentences.
- Do not "sound professional" by copying English corporate calques into another language.
- Thai, Japanese, Arabic, Spanish, and every other pack: load register examples from `references/languages/<id>/registers.md`, then keep vocabulary and grammar **simple within that register**.
- When the pack is thin or uncertain, fall back to plain coworker clarity and state limits honestly — do not inflate complexity to hide uncertainty.

## When complexity is OK

Keep simple prose as the default even here; add complexity only when the task requires it:

| Situation | Guidance |
|---|---|
| Legal, compliance, or contract text | Use required legal terms; still prefer short sentences where the format allows |
| Academic use case (`usecases/academic`) | Follow discipline conventions; avoid empty jargon that adds no precision |
| Quoted technical terms, error messages, API names | Copy byte-for-byte; simplify only the prose around them |
| User explicitly asks for formal / `baku` register | Use correct formal forms; do not add rare vocabulary or nested grammar for show |
| Domain terms the repo already uses | Keep them; wrap in simple sentences |

---

## Agent rules (MUST / MUST NOT)

### MUST

- Default to common words and short, complete sentences in every language.
- Put the main point in sentence 1 when explaining, warning, or updating.
- Use active voice and name the actor when known.
- Define acronyms once, then use the short form.
- Match register with appropriate **forms**, not with inflated vocabulary or grammar.
- Apply this bar before anti-slop thinning — simple draft first, then cut AI clusters.

### MUST NOT

- Replace a plain verb with corporate jargon when a common word works in that language.
- Stack subordinate clauses, passives, or hedges to sound "smart" or "professional."
- Pick rare, literary, or dictionary-heavy words just because the register is formal.
- Treat formal register as a license for long, nested sentences.
- Leave acronyms undefined on first mention in user-facing prose.
- Write prose that needs a second read to find who did what or what happens next.
- Bulk-edit protected artifacts (code, commands, paths, quoted errors) to "simplify" them.
- Default to em dash for asides, chaining, or punch — use comma, period, colon, or parentheses instead.

---

## Quick self-check (with [evaluation.md](evaluation.md))

Before delivery on important prose:

1. Could a tired teammate parse this in one read?
2. Is any word replaceable with a shorter common synonym without losing meaning?
3. Does each sentence carry one main idea (or one clear list job)?
4. Would reading aloud require a breath mid-clause? Split it.

See also [techniques/natural-writing.md](techniques/natural-writing.md) for rewrite and calque passes.
