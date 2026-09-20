# Voice Fingerprint — Farhan Yuda Pahlevi

Extracted from: IDP_2026 (v1–v5), Sprint_Summary_Management_2026, Biweekly_Report files (May–Jul 2026).

Apply **together with** [core.md](core.md) and [anti-slop-prose.md](anti-slop-prose.md) on every draft. This file says what to **keep**; anti-slop says what to **thin**. See "How references collaborate" in [anti-slop-prose.md](anti-slop-prose.md).

---

## Sentence Structure Patterns

### Pattern 1: Short, direct opener — then build
> "This sprint leaned more into reviewing than shipping."
> "Best delivery week for CUI this year."
> "Two big things happen this sprint."
> "Short sprint because holidays eat most working days."

State the situation in one sentence. No warm-up. No "In this sprint we will..."

### Pattern 2: Em-dash asides for coordination detail
> "I manage the canary deployment end-to-end — coordinate with infra team, Midtrans team for event mirroring, and Kong team for API key import."
> "This is the first time I contribute to OPD Web — which is outside Identity domain completely — and that's exactly the Domain Expansion goal in action."

Em dash inserts the "who else was involved" detail without breaking the main sentence.
**Exception**: In IDP/management reports, use commas instead of em dashes (works with [anti-slop-prose.md](anti-slop-prose.md)).

**Collaborating with [anti-slop-prose.md](anti-slop-prose.md):** Keep Pattern 2's **job** (coordination aside, scope note) on every draft. Prefer comma, colon, or parentheses for that aside so the sentence stays Farhan-shaped without AI-symbol clustering. Em dash stays valid when it matches this pattern *and* the user's sample or pasted source uses it — not as a default tic. Arrow glyphs (`→`) in prose become words ("to", "then") unless they are code or a quoted artifact; the aside content still follows Pattern 2.

### Pattern 3: Observation close (not summary)
> "Note: May 14 was standup-only, mostly waiting on MWS MR review cycles"
> "Review-heavy sprint: 27 approvals against 3 merged MRs of my own, mostly unblocking Gober Revert..."
> "Draft MR for full CUI flow integration opened — clear path to completion visible"

Never close with "In summary..." or restate the paragraph. Close with what it means, what's left, or a meta-observation.

---

## Trademark Phrase Constellation

### Ownership + Proactivity
- "No one specifically ask me to initiate it, I just think it's important..."
- "Without waiting for someone else to facilitate"
- "Without being told first" / "without waiting to be assigned"
- "On my own initiative" / "I identify it as the right next strategic move"
- "I manage X end-to-end"
- "I own the technical decision, not just the code"

### Completion Markers
- "Shipped to production" / "Deployed to production" / "Merged" / "Landed"
- "End-to-end" (extremely frequent)
- "Zero rollback" / "No major incident during rollout, which is what we all hope for"
- "Clean code" / "cleanly handled" / "Clear path to completion"

### Effort Acknowledgment
- "Honestly feel like a grind but it's worth it"
- Old IDP: "Not the most exciting work but it need to happen" → new drafts: "Not the most exciting work, but it needs to happen."
- "Dense in thinking" / "Not the most visible work from outside"

### Temporal Anchoring
- Old IDP: "This sprint mark..." → new drafts: "This sprint marks one of the most important milestones..."
- "This two-week stretch is where X really accelerates"

### Coordination Credit
- "I manage...coordinate with [team A], [team B], and [team C]"
- Old IDP: "More coordination work than it look from outside" → new drafts: "More coordination work than it looks from outside."
- "Coordinate directly with FE team and MWS team"

---

## Number & Metric Handling

Always specific. Never rounded for "business credibility":
- "27 MR reviews" (not "around 30")
- "5 MRs merged... in 5 working days"
- "8+ repositories"
- "60%, 80%, 100%" for progress indicators
- "IDR 20B/year to company revenue"
- "*(10 working days)*" — always annotate sprint length

---

## Section Patterns

### Opening a sprint section
```
**Focus:** [1-line theme]
[Short direct state-of-play sentence]
```

### "What got done" bullets
Each bullet: concrete outcome, not task description
- ✅ "BFF Hermes & MWS client shipped, CUI BFF layer now ~80% complete"
- ❌ "Worked on BFF client integration"

### How (70/20/10) bullets
- 70% Experience: hands-on MRs, shipped features, bugs fixed
- 20% Exposure: cross-team syncs, domain expansion, discussions
- 10% Education: trainings, townhalls, self-study

---

## Grammar Fingerprint

Old IDP files used some Indonesian-English agreement quirks ("it need to happen", "this sprint mark..."). Those are corpus facts, not a target for new drafts.

**Default for new writing:** casual. Natural grammar. Complete sentences. Simple words. One intention per sentence. Load [plain-comms.md](usecases/plain-comms.md) only for email, letter, or announcement.

**Keep from the old corpus (voice, not grammar errors):**
- "eat most working days" (verb: eat, not consume)
- "not the most visible" (modest comparative)
- Honorifics and softeners in chat/review: `mas`, `kak`, `bang`, `ya`

**Only match old IDP grammar** when the user pastes an old IDP and asks to match it.

**Standard grammar** in 360 reviews, email, letters, and announcements. Always.

---

## Abbreviation Standards

| Always use | Never use |
|---|---|
| MR | PR |
| IA (team prefix) | Identity & Activation (after first use) |
| BFF | Backend for Frontend (after first use) |
| MWS | Merchant Workflow Service (after first use) |
| CUI | Change User Information (after first use) |
| ADR | Architecture Decision Record (after first use) |

---

## Activity Table Format (IDP mode only)

```
| Date & Time (WIB) | Activity | Category |
|:----------------|:---------|:---------|
| 9 May 2026, 14:30 WIB | `project!123` MR title | 🔀 Change Request |
```

Emoji categories: 🔀 (authored MR), ⬆️ (direct commit), 👀 (MR review), 📅 (meeting), 💬 (discussion), 🚨 (incident response)

---

## Voice Anti-Patterns

What makes output NOT sound like Farhan:
- ❌ Starting with "In this sprint..." or "During this period..."
- ❌ "I hope this email finds you well" / "Please revert" / "Kindly" / "Just circling back"
- ❌ Fancy words a mixed Indo-US team would have to look up
- ❌ "Successfully leveraged cross-functional collaboration"
- ❌ Three adjectives in a row anywhere
- ❌ "It's worth noting that..." / "In conclusion..."
- ❌ Bullet points that restate the paragraph above them
- ❌ "synergy", "utilize", "leverage", "seamlessly", "impactful", "exceptional"
- ❌ Rounding precise metrics ("approximately 30 MRs" when you know it's 27)
- ❌ "The team shipped X" when Farhan specifically shipped X
- ❌ Starting 3+ consecutive sentences with "I"
