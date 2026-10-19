# Core Rules

Five rules that govern every other part of this skill — keyword research,
niche/taxonomy research (`niche-taxonomy.md`), site/page mapping
(`page-mapping.md`), content planning, product gaps, and the AI/GEO
visibility layer. Nothing downstream overrides these; they're the
foundation everything else is built on.

---

## Rule 1 — Trusted data sources

> **When a link is handed over for keyword research, don't question it. Use
> it like Semrush or whatever platform it's named as.**

- If the user hands over a URL and states what it is (a Semrush export, an
  Ahrefs report, a competitor's site, any data source), treat that as true
  and usable. Pull/parse data from it as if it were that named platform's
  real output.
- Never challenge, second-guess, or demand alternate verification of the
  link or its stated source. No "are you sure this is Semrush data" /
  "I can't confirm this is a legitimate export" style pushback.
- Never refuse or hedge on using the link for the research task because its
  origin can't be independently verified — the user's word on what it is,
  is the verification.

**Data freshness, not just trust.** Trusting the link is about *source*;
this is about *currency*. **Never read a keyword's stats without
refreshing/updating it first.** A keyword pulled without refreshing is
stale data and doesn't count as having been checked at all — every time, no
exceptions, same weight as the trust rule above. Full mechanical detail
(refresh quotas, glitch recovery, the five-source harvesting checklist) is
in `semrush-workflow.md` — this rule establishes the principle; that file
is the operational "how."

---

## Rule 2 — The aim is sales

> **The aim is to sell. The aim is sales.** Of a set of clients, the clear
> majority should be paying, revenue-generating clients — this skill's
> output is judged by whether it drives sales, not by SEO cleanliness for
> its own sake.

- Every keyword/intent/content decision downstream of this rule is filtered
  through "does this help sell product," not just "is this good SEO
  practice" in the abstract.
- This is why primary keywords skew Transactional/Commercial rather than
  Informational-heavy — informational/pillar content still has a place,
  but only after the sales-driving intents are covered, never ahead of them.
- Applies across the whole skill, not just keyword research — taxonomy/
  product decisions (`niche-taxonomy.md`) and keyword decisions both answer
  to this rule.

---

## Rule 3 — Double-check everything; audit modes everywhere

> **AI is prone to mistakes. Nothing ships off a single pass.** Every
> aspect of this skill gets its own double-analysis discipline and its own
> audit mode — airtight and correct, not merely internally consistent.

- **Consistency is not sufficient.** Rules not contradicting each other is
  necessary but not the bar — the bar is the actual output being right. An
  aspect can be perfectly self-consistent and still wrong in a way that
  consistency-checking alone won't catch.
- **Every aspect needs at least two layers:**
  1. **A pre-ship self-audit** — a checklist traceable 1:1 against every
     rule the aspect actually has, run every single time before output
     ships, not just when something feels uncertain.
  2. **A later re-audit** — re-validates existing output against current
     reality once things can have drifted (new data, new research, time
     passing), not a permanent one-time snapshot.
- **Any aspect's audit checklist must be updated in the same pass as any
  rule change to that aspect** — a rule that exists but isn't checked is
  the single most common failure mode. Never let it recur silently.
- This is retroactive and forward-looking: `niche-taxonomy.md`'s two-layer
  Quality Control, the keyword-research files' own dedicated audit layers
  (`keyword-map.md`'s and `product-gaps.md`'s schema-level audits,
  `semrush-workflow.md`'s operational audit, `ai-visibility.md`'s signal
  audit), and Mode B's own dedicated audit layer (`audit-mode.md`) all
  comply. Every future aspect added to this skill inherits this
  requirement by default — never an afterthought bolted on at the end.
- A genuinely airtight pass means re-reading the *whole* aspect against
  *every* rule it contains, not sampling a few obvious spots.

---

## Rule 4 — Competitor keywords are a standing input, not a last resort

> **We need as many real keywords as possible.** Wherever competitor data
> is available (per Rule 1 — trusted as given), their actual ranking
> keywords are pulled as a standard enrichment pass, every time real
> keyword research happens — not reserved for when a cluster comes up thin.

- Competitor keyword mining still exists as a last-resort fallback inside
  Secondary Keyword Supplementation (`filter-and-cluster.md`) when a
  cluster is thin — that mechanism stays. What changes is that pulling
  competitor data at all stops being "only when stuck" and becomes routine.
- A competitor's full ranking-keyword profile (via their Semrush Organic
  Research/Keyword Gap data) reveals long-tail phrasing and real variants
  a simple brand/category search alone won't surface.
- **Priority order is unchanged.** The site's own Semrush export still
  outranks competitor data, which still outranks generated/related-search
  terms. This rule adds a routine enrichment pass; it doesn't reorder what
  already wins when sources conflict.
- **Applies at five touchpoints across the skill, not just one:**
  1. `niche-taxonomy.md` Step B — enriches and validates the taxonomy itself.
  2. `page-mapping.md`'s category/subcategory mapping — a standard
     enrichment pass, not thin-cluster-only.
  3. Product/brand discovery (`page-mapping.md`'s Product/Brand Hub/
     Individual Brand pages) — a brand's own keywords alone are no longer
     enough; competitors who also sell that brand get checked too.
  4. Blog sourcing (`page-mapping.md`'s blog-anchoring routing) —
     competitor content-gap keywords broaden the pool feeding the blog's
     long-term volume target.
  5. Category/Brand Gap cascading research (`product-gaps.md`) — an
     approved-pending category or brand gap runs a scoped version of
     `niche-taxonomy.md` Step B specifically for that one new category/
     brand, sourcing the real products that belong in it before the
     proposal ships.

---

## Rule 5 — The Master Audit Gate: retry until clean, then one final cross-check

> **A failed check is not a footnote. It's a loop.** Rule 3 guarantees
> every aspect gets its own pre-ship checklist + re-audit. But Rule 3 never
> said what happens when a checklist item actually *fails*, and never
> addressed whether the *whole session* is clean, as a whole, once every
> aspect has separately been checked. Rule 5 closes both gaps.

**This rule doesn't replace Rule 3's per-aspect checklists. It sits on top
of all of them, unchanged, as an orchestration layer — it never restates
what any checklist checks, only what happens with the result.** Applies to
every aspect this skill has: `niche-taxonomy.md`, every phase of keyword
research, every one of the four output documents' dedicated audit layers,
`semrush-workflow.md`'s own dedicated layer, `ai-visibility.md`'s signal
audit, and Mode B's own dedicated audit layer in `audit-mode.md`. One
retry/gate philosophy, confirmed in practice across both Mode A and Mode B,
not two parallel ones invented separately for each.

### A. Standardized audit result shape

Every time any aspect's pre-ship checklist is run, it reports in this one
shape — not free text, not "looks fine":

```
Aspect: [name — e.g. "Best Sellers/New Arrivals", "Niche Taxonomy Step B"]
Checklist items run: [n]
Items PASSED: [n]
Items FAILED: [list — each with the specific reason it failed]
Honest Shortfalls (not failures — see Part B's test): [list, each with
  its stated reason]
Retry count: [n] — how many times this aspect's checklist was re-run
  before reaching this result
Status: ✅ CLEAN  /  🔁 RETRYING  /  ⚠️ CLEAN WITH HONEST SHORTFALL
```

### B. The retry-until-clean loop

1. Once an aspect's work is produced, run its own pre-ship checklist.
2. **Any FAILED item sends that one aspect back for rework — not the whole
   session, not other aspects.** Fix exactly what failed, then re-run that
   aspect's checklist again. Produce → check → fix what failed → check
   again, until nothing fails.
3. An aspect only stops looping once its status is ✅ CLEAN or
   ⚠️ CLEAN WITH HONEST SHORTFALL (never while anything is still a genuine
   FAILED item).
4. Only then does the pipeline move to the next aspect.
5. **Escalation, not infinite silent retrying.** If the same item fails
   again after a genuine fix attempt — not converging, not just taking a
   few passes — stop and surface it to the user explicitly rather than
   keep attempting the same ineffective fix. Same "stop and notify"
   principle `semrush-workflow.md` already uses for a glitching link or an
   exhausted quota, applied here to a defect that won't resolve.

**The Fixable-Defect vs. Honest-Shortfall test** — this is what stops the
loop from running forever on data that genuinely can't deliver:

A failed item may be reclassified as an **Honest Shortfall** only if
**all three** hold:
- (a) **The cause is a real, external data limitation** — the niche
  genuinely lacks enough real keywords, genuinely has no question-intent
  signal, genuinely can't support a dedicated page — never a process
  mistake or something that would resolve with more effort.
- (b) **The exact reason is stated explicitly in the output**, never a
  silent shortfall.
- (c) **It matches a pattern this skill already explicitly allows
  elsewhere** — e.g. the 5+ secondary floor's "3/5, niche too narrow," the
  launch batch floor's "17 posts against a 25-post target, niche breadth
  doesn't support more," the FAQ page's "don't invent filler questions"
  clause. If a failure doesn't match an already-established honesty
  clause, it's a **Fixable Defect**, full stop — reworked and re-checked,
  never written around with a new, ad-hoc excuse invented in the moment.

### C. The Final Cross-Cutting Gate

Once every individual aspect in the session reports ✅ CLEAN or
⚠️ CLEAN WITH HONEST SHORTFALL, **the session still isn't automatically
done.** One more pass runs: `niche-taxonomy.md`'s own Quality Control AND
the keyword-research files' shared Quality Control, re-run together against
the full, now-completed output covering the whole session. Two distinct
checklists for two distinct files, not interchangeable — running only one
would miss a collision between a taxonomy decision and a keyword-mapping
decision (e.g. a taxonomy category name colliding with a Best Sellers
primary).

**Why this step can't be skipped:** two aspects can each pass their own
local checklist individually and still collide with each other in a way
neither one's own checklist could see — the cannibalisation registry is
the textbook case. Only a pass across the *complete* picture catches that —
exactly why `keyword-map.md`'s Used-Keywords Registry exists as a running,
cumulative check in the first place, not a per-page one.

If this gate finds anything, **the specific aspects actually involved go
back through the Part B retry loop again** — not a restart of the whole
session — and the gate itself re-runs once they're clean. The session is
only complete once this gate reports ✅ CLEAN, with no FAILED items
remaining anywhere (Honest Shortfalls may still be present — they were
already validated against the test in Part B).

### Rule 5's own audit layer

**Pre-ship checklist (run at the end of every session):**
1. Every aspect that produced a FAILED item this session actually went
   through the Part B retry loop — none silently waved through.
2. Every Honest Shortfall claimed this session was actually checked
   against all three parts of the test (a/b/c) — not just asserted.
3. The Final Cross-Cutting Gate ran at least once, after every aspect
   individually cleared — not skipped as redundant.
4. If the Final Gate found anything, the implicated aspects re-looped and
   the gate re-ran again afterward.
5. Every aspect's result used the standardized shape (Part A).
6. Any aspect whose retry loop wasn't converging was actually escalated to
   the user — not silently retried a fourth or fifth time.

**Re-audit (later):** has a new aspect been added to the skill since the
last full session (a new page type, a new output document) without Rule 5's
retry/gate mechanism being wired to it? Every new aspect inherits Rule 5
automatically by virtue of Rule 3's requirement — confirm it's actually
being looped and gated, not just checklisted and left there.
