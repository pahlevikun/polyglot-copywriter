# Humanize workflow

Operational humanize loop. **Extends** [anti-slop-prose.md](../anti-slop-prose.md) with detect → rewrite → verify — do not duplicate the full pattern tables; cross-link instead.

Load when use case is `humanize`, or user asks to de-AI, humanize, rewrite stiff copy, or audit for AI tells.

## Two modes

| Mode | User intent | Output |
|---|---|---|
| **Edit** (default) | Fix a draft | Rewritten text + short "what changed" |
| **Detect** | Audit only | Named patterns, quoted lines, fix hint — no rewrite until asked |

If no draft, ask for one. If audience/format unclear, ask once: who is this for and where will it publish?

## Loop: detect → rewrite → verify

```
1. READ full draft — note voice traits to keep (cadence, bluntness, humor, uncertainty)
2. DETECT — scan [anti-slop-prose.md](../anti-slop-prose.md) clusters + checklist below
3. REWRITE — minimum effective edit; preserve meaning and personal markers
4. VERIFY — re-read aloud; run quick score from [evaluation.md](../evaluation.md) § Self-check rubric
5. DELIVER — edited draft + what changed (edit mode) or findings list (detect mode)
```

**Rule:** Look for **clusters**, not isolated tells. One em dash or one "however" is fine. Em dash + rule of three + empty vocabulary + generic kicker in one paragraph is a cluster.

## Core rewrite principles

1. **Preserve the writer's real voice** — Do not sterilize into generic polished prose.
2. **Minimum effective edit** — Strong human sentences stay.
3. **Lead with the point** when setup adds nothing; keep asides that create context or character.
4. **Never invent** claims, stats, examples, or sources.
5. **Portability test** — If a sentence could move unchanged to another company/product, cut or replace with a specific fact.
6. **Show, don't tell importance** — Cut "the key point is" / "this matters because" when the prose already shows it.
7. **Trust the reader** — Skip softening, hand-holding, and interpretive metadiscourse.

## Pattern quick reference (audit)

Use [anti-slop-prose.md](../anti-slop-prose.md) for full tables. High-signal audit list:

| Category | Examples |
|---|---|
| **Empty vocabulary** | delve, leverage, robust, seamless, tapestry, landscape (abstract), foster, elevate |
| **Binary contrasts** | "It's not X, it's Y" / "Not just X but Y" — state Y directly |
| **Colon reveals** | "The detail that matters: a separate agent grades it" — use plain sentences |
| **Trailing -ing** | "…highlighting their commitment" — cut or replace with mechanism |
| **Significance inflation** | pivotal moment, testament, new era, revolutionizing |
| **Weasel attribution** | experts say, studies show — name source or cut |
| **Fake-profound kickers** | Mic-drop metaphor at end — end on last concrete fact |
| **Summary recap** | "In conclusion…" / restating the whole piece |
| **Formatting slop** | emoji headings, bold every keyword, bullets where prose fits |

## Inject soul (not just scrub)

After thinning clusters, check the draft is not **technically clean but lifeless**:

- Mixed sentence length (not robotic rhythm)
- Specific detail or honest uncertainty where appropriate
- Point of view when the channel allows
- Do not make every paragraph equally tidy

## Collaboration with other refs

| Reference | Role in humanize pass |
|---|---|
| [anti-slop-prose.md](../anti-slop-prose.md) | Pattern catalog + symbol hygiene |
| [voice-fingerprint.md](../voice-fingerprint.md) | Keep Farhan markers (EN/ID) |
| [core.md](../core.md) | Register, vocab, protected artifacts |
| [english-humanizer.md](../usecases/english-humanizer.md) | Extended EN pattern library |
| [natural-writing.md](natural-writing.md) | Plain sentence + calque pass (all langs) |

## Detect-mode output shape

For each hit:

```
- **Pattern:** {name from anti-slop or table above}
- **Quote:** "{line}"
- **Fix:** {one-line direction}
```

Offer to run edit mode after detect.
