# Output Format Templates

All four documents are produced at the end of every keyword engine session. They are designed to be read independently and used directly by code/build workflows.

---

## Document 1: keyword-map.md

```markdown
# Keyword Map — [Site Name] ([Market: US/UK])
**Generated:** [Date]
**Total Keywords Processed:** [n]
**Keywords Kept (Primary, KD ≤28):** [n]
**Keywords Kept (Secondary, 29–35 fallback band only):** [n]
**Keywords Dropped (above KD 35 — no exception):** [n]
**Clusters Created:** [n]
**Pages Mapped:** [n] existing / [n] new
**Secondary-Floor Compliance:** [n]/[n] pages at 5+ secondaries ([n] supplemented, [n] under floor and flagged honestly — see Per-Page section)

---

## Keyword Allocation Table

| Cluster | Primary Keyword | Vol | KD | Tier | Intent | Secondaries (5+ min) | Assigned URL | Page Type | Status | FAQ Schema | Entity Gaps | Speakable | SERP Feature |
|---------|----------------|-----|----|------|--------|----------------------|-------------|----------|--------|-----------|-------------|-----------|--------------|
| [name] | [keyword] | [v] | [k] | T1 | Trans | 6/6 | /url/ | Product | Existing | Yes | None | Yes | Snippet — table |
| [name] | [keyword] | [v] | [k] | T2 | Comm | 5/5 (2 supplemented) | /url/ | Blog | New | No | Brand | No | PAA — 3 folded into FAQ |

---

## Per-Page On-Page Requirements

### [Page URL]
- **Guarantee Flag:** Yes (built because it must exist) / No (pre-existing page, mapped onto — not created by any Guarantee mechanism) / Active-Conditional (Sale/Best Sellers/New Arrivals/Compare/Wholesale, currently active)
- **Intent-Chain-Used:** [which of T/C/N/I actually won for this primary — not assumed, the one that genuinely won the tie-break]
- **Source Note:** [why this page exists — e.g. "Category/Subcategory Guarantee," "Approved Category Gap," "Active Sale trigger," "Pre-existing page, mapped"]
- **Title Tag:** [formula output — max 60 chars]
- **H1:** [formula output]
- **Meta Description:** [formula output — 130–155 chars. This band satisfies both Google (≤160) and Bing (120–158). Target ~148 chars.]
- **Primary Keyword:** [keyword] (Opportunity Score: [n])
- **Secondary Keywords (5+ minimum — homepage and shop page: 3-5):** [kw1], [kw2], [kw3], [kw4], [kw5] [related-search], [kw6] [generated] — tag every supplemented keyword with its source (`[site-search]` / `[competitor]` / `[related-search]` / `[generated]`); untagged = export-backed real data
- **LSI/Supporting Keywords:** [list]
- **Image Alt Text:** [primary keyword — product detail]
- **Journey Stage:** Awareness / Consideration / Purchase / Loyalty
- **Internal Links OUT:** [URL — anchor text], [URL — anchor text] — for Informational/Commercial content, this is the journey-stage forward link to the Transactional page(s) it should funnel toward (multiple pages allowed, not a single value)
- **Internal Links IN:** [URL — where/how to link here] — for a Transactional page, the journey-stage back link from relevant Informational/Commercial content when it exists
- **FAQ Schema:** Yes / No
- **Page-Level FAQ (if FAQ Schema = Yes, 2–4 Q&As — `content-planning.md` § Page-Level FAQ):**
  - **Q:** [Question] **A:** [40–65 word answer, includes a keyword naturally, ends with a link/CTA]
  - [Repeat, 2–4 total]
- **Speakable Target:** [CSS class e.g. `.faq-answer-speakable` / `.brand-statement`] / N/A — WebForge adds this class to the element during build
- **Entity Coverage:** ✅ Product | ✅ Brand | ✅ Category | ⚠️ Location missing
- **Definition Hook:** [1–2 sentence hook draft — place in first 150 words of page] — AI-citation formatted: fact-first, one claim per sentence, number anchored early
- **SERP Feature:** [Detected feature — Snippet (paragraph/list/table) / PAA / Image pack / Shopping pack / None] → [structural response applied — e.g. "comparison table added," "3 PAA questions folded into page FAQ"]
- **WebForge Schema Type:** Article / HowTo / FAQPage / Product / Review / Organization — tell WebForge which JSON-LD type this page needs beyond its defaults

[Repeat for every mapped page]

---

## Dropped Keywords (KD above 35 — nothing here is used anywhere)

**No Supporting Pool, no Revisit-in-6-Months appendix — both removed.** The KD ceiling is now a hard rule: primaries never exceed 28 (no fallback), secondaries default to ≤28 with a 29–35 fallback used only when genuinely needed to hit the secondary minimum, and **nothing above KD 35 is used anywhere, under any exception** — not enriched into body copy, not held for revisit, not appended as a reference list. A keyword above 35 is dropped, full stop, regardless of its volume. List it here only as a record of what was found and excluded, not as a usable resource:

| Keyword | Vol | KD | Reason Dropped |
|---------|-----|-----|-------|
| [keyword] | [v] | [k] | Above KD 35 ceiling — no exception applies |

---

## Orphan Keywords (for manual review)
| Keyword | Vol | KD | Why Orphaned |
|---------|-----|-----|-------------|
| [keyword] | [v] | [k] | Single keyword, no cluster match |
```

### Quality Control — `keyword-map.md`'s own dedicated audit layer

Governed by Rule 5 (`core-rules.md`). The schema above has enough distinct fields, and enough ways one of them can be silently skipped, to warrant its own checklist rather than relying on the general Mode A Quality Control alone.

**Pre-ship checklist (run before `keyword-map.md` ships, every session):**
1. Every mapped page has a **Guarantee Flag** value, and it's the correct one — Yes only for a page actually built because a Guarantee required it, Active-Conditional only for a currently-live Sale/Best Sellers/New Arrivals/Compare/Wholesale trigger, never left blank or defaulted to No.
2. **Intent-Chain-Used** records which intent genuinely won the tie-break for that page's primary — not assumed from the page type.
3. Every page has a **Journey Stage** value, and its **Internal Links OUT/IN** actually reflect the bidirectional linking requirement (`page-mapping.md` § Journey-Stage Internal Linking) — not left as a single-direction note or omitted.
4. **FAQ Schema = Yes** pages all carry an actual **Page-Level FAQ** field with 2–4 Q&As — never Yes with no content, never invented filler where the cluster has nothing to draw on.
5. **Secondary-Floor Compliance** in the header matches what the Per-Page sections actually show — every page under the 5+ floor (3+ homepage/shop) is both counted in the header *and* has its shortfall stated honestly in its own Per-Page entry, not just one or the other.
6. Every supplemented secondary carries its source tag (`[site-search]`/`[competitor]`/`[related-search]`/`[generated]`); untagged keywords are genuinely export-backed, not supplemented keywords with a dropped tag.
7. **SERP Feature** and **WebForge Schema Type** are filled per page, not left as a generic default repeated everywhere — a page with no detected SERP feature says "None," it isn't just skipped.
8. The Used-Keywords Registry (Rule 5's Final Cross-Cutting Gate depends on this) was actually checked page-by-page as pages were added, not reconstructed from the finished table after the fact.

**Re-audit (later, same trigger pattern as every other Layer 2 in this skill):**
- Has a page's Guarantee Flag drifted from reality (an Active-Conditional trigger ended, a new one started)? `audit-mode.md`'s Guarantee Flag check is the live-site version of this — confirm it's actually catching drift, not just checking presence.
- Has any page's Journey Stage or linking gone stale as new pages were added after the original mapping? New pages need their forward/back links retrofitted, not left orphaned from the link graph.
- Has a Reason-A or Reason-A2 blog-routed keyword grown past its orphan threshold (vol 100/200) since this was last generated? Promote it out of blog if so.

---

## Document 2: blog-plan.md

**`blog-plan.md` now absorbs the old `keyword-cluster.txt`'s job too — one document, not two.** Every post row carries a **Status** field (`Pending` / `Built`), flipped to `Built` once WebForge actually publishes that post. WebForge reads this one file for both the brief content and the build queue (next unused post = next `Pending` row in priority order); there is no separate companion file anymore.

**Launch batch floor is tiered by niche breadth, not a flat 20 — see the sizing proxy table in content-planning.md § Launch Batch Floor:**

| Niche tier | Launch batch (ready at go-live) | Reserve pipeline (toward 1000+) |
|---|---|---|
| Micro/Small | 25–30 | Remainder, ongoing |
| Medium | ~40–60 | Remainder, ongoing |
| Large | ~70–100 | Remainder, ongoing |
| Massive | 100+ | Remainder, ongoing |

```markdown
# Blog Plan — [Site Name] ([Market: US/UK])
**Generated:** [Date]
**Niche Tier (content-planning.md's sizing proxy):** [Micro/Small/Medium/Large/Massive]
**Total Blog Posts Planned:** [n] — launch batch target [n] per the tier table above ([n] scheduled in the first 12-week window, [n] queued in the backlog beyond it, toward the 1000+ overall target where the niche supports it)
**Pillar Posts:** [n]
**Standard Posts:** [n]
**Launch Batch Floor:** ✅ Met ([n] briefed against a [n] target) / ⚠️ Short ([n] briefed — see note on why genuine expansion couldn't reach the tier's target)

---

## 12-Week Content Calendar (First Window — Backlog Continues Beyond Week 12)

| Week | Post Title | Primary Keyword | Type | Funnel | Tier | Words | WebForge Schema | Status |
|------|-----------|----------------|------|--------|------|-------|----------------|--------|
| 1 | [title] | [keyword] | [type] | Bottom | T1 | [n] | Article + FAQPage | Pending |
| 2 | [title] | [keyword] | [type] | Bottom | T1 | [n] | Article + HowTo | Pending |
[...]

**Status column:** `Pending` / `Built` — flipped to `Built` once WebForge actually publishes that post. This is the field that replaces the old `keyword-cluster.txt` queue — WebForge reads it directly from this table, there's no separate file to keep in sync.

**WebForge Schema column key:**
- `Article` — standard blog post (default in WebForge seo.md)
- `Article + FAQPage` — post has FAQ section; WebForge nests FAQPage schema inside Article
- `Article + HowTo` — how-to guide; WebForge wraps steps in HowTo schema
- `Article + Review` — product review post; WebForge adds Review schema
- `Article (Pillar)` — pillar post; WebForge adds extra Article `mentions` and `about` fields

---

## Pillar Posts (Start Writing Week 1 — Publish Week 4/8/12)

[Full brief for each pillar — see brief template in content-planning.md]

---

## Standard Blog Posts (T1 — Publish Weeks 1–4)

[Full brief for each post]

---

## Standard Blog Posts (T2 — Publish Weeks 5–12)

[Full brief for each post]

---

## Backlog Posts (Beyond Week 12)

All remaining briefed posts that didn't fit the first 12-week window — full briefs, same completeness as any scheduled post, ready to build whenever capacity allows. These are sequenced in this same document (with their own `Pending`/`Built` Status), not held back for a future session and not in a separate file.

[Full brief for each backlog post]

---

## Internal Linking Architecture

[Diagram/table showing which posts link to which — pillar → clusters → products]
```

---

## Document 3: faq-bank.md

```markdown
# FAQ Bank — [Site Name] ([Market: US/UK])
**Generated:** [Date]
**Total Questions:** [n]
**Homepage FAQ Questions:** [n]
**FAQ Page Questions:** [n] across [n] themes

---

## Homepage FAQ (6–8 Questions)
These go in the FAQ section on the homepage. Short, buyer-focused, objection-removing.

**Q: [Question]**
A: [40–55 word answer. Concrete. Includes keyword. Ends with CTA or link.]

[Repeat for all homepage FAQ questions]

### Homepage FAQPage Schema Block
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "[Question]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Answer]"
      }
    }
  ]
}
```

---

## Full FAQ Page Bank

### [Theme 1: e.g. About Our Products]

**Q: [Question]** ⭐ [Speakable — mark best answer per theme]
A: [50–65 word answer]

**Q: [Question]**
A: [50–65 word answer]

[Continue...]

### [Theme 2: Ordering & Shipping]
[...]

### [Theme 3: Safety & Age]
[...]

### FAQPage Schema Block — Full FAQ Page
[Complete JSON-LD block with all questions]

---

## Blog Post FAQ Sections
[List of which FAQ questions belong in which blog post brief — cross-reference with blog-plan.md]
```

---

## Document 4: product-gaps.md

```markdown
# Product Gap Analysis — [Site Name] ([Market: US/UK])
**Generated:** [Date]
**Total Gaps Found:** [n]
**Brand Gaps:** [n]
**Product Gaps:** [n]
**Category Gaps:** [n]
**Accessory Gaps:** [n]
**Competitor Gaps:** [n] (only if a competitor SEMrush export was provided — otherwise state "Not run — no competitor export provided")

---

## Priority Matrix

| Gap Name | Type | Demand Signal | CPC Signal | Recommended Price | Priority | Est. Revenue Potential |
|----------|------|--------------|-----------|-------------------|----------|----------------------|
| [name] | Brand | [combined vol] | High | [single recommended price, from competitor research] | T1 | High |
| [name] | Competitor | [combined vol] | Medium | [single recommended price, from competitor research] | T2 | Medium |
[...]

**Recommended Price** is the price-tiered-volume criteria's output — a single number per gap, sourced from competitor pricing research, not a range. Re-check it before an approval if competitor pricing has moved since this was generated (it goes stale the same way any competitive data does).

---

## T1 Gaps (Act First)

[Full proposal for each T1 gap — see product-gaps.md template]

---

## T2 Gaps (Next Phase)

[Full proposals]

---

## Accessory Gaps

[Full proposals grouped by accessory type]

---

## Competitor Gaps (only if a competitor export was provided)

[Competitor Gap Summary table + full proposals — see product-gaps.md § Competitor Gap Analysis]

---

## Competitor Brand Opportunities

[List of competitor brand keywords found, with comparison content recommendations]

---

## 🔗 Link Magnet Candidates

[1–2 realistic candidates with type, rationale, and format — see product-gaps.md § Link Magnet Candidates. State plainly if none identified this session.]

---

## llms.txt Priority Map

### P1 — Always Include
[list]

### P2 — High-Value Pages
[list]

### P3 — Content Pages
[list]

### Exclude
[list]
```

---

## Document 5: deprecated — merged into blog-plan.md

`keyword-cluster.txt` no longer exists as a separate file. The problem it solved (giving WebForge a flat, easy-to-scan build queue) is now solved inside `blog-plan.md` itself via its per-post `Status` (`Pending`/`Built`) field, documented in Document 2 above. Only four real documents are produced now: `keyword-map.md`, `blog-plan.md`, `faq-bank.md`, `product-gaps.md`.

---

## In-Chat Session Summary

At the end of every session, output this summary in chat before delivering the files:

```
## ✅ Keyword Engine — Session Complete

**Site:** [domain] ([market])
**Session Date:** [date]

### What Was Processed
- Raw keywords received: [n]
- Keywords kept (primary, KD ≤28): [n]
- Keywords kept (secondary, 29–35 fallback band only): [n]
- Keywords dropped (above KD 35 — no exception applies): [n]

### What Was Built
- Keyword clusters created: [n]
- Existing pages mapped: [n]
- New pages needed: [n] (see product-gaps.md)
- Secondary-keyword floor: [n]/[n] pages at 5+ secondaries — [n] needed supplementation ([n] site-search, [n] competitor, [n] related-search, [n] generated), [n] shipped honestly under floor
- Programmatic page sets flagged: [n] (only if the catalog has genuine combinatorial scale — otherwise omit)
- Blog posts planned: [n] ([n] pillar, [n] standard) — launch batch floor (per niche tier): ✅ Met / ⚠️ Short ([n] scheduled in first 12 weeks, [n] in backlog toward 1000+)
- FAQ entries generated: [n] ([n] homepage, [n] full page)
- Product gaps identified: [n] ([n] brand, [n] product, [n] category, [n] accessory, [n] competitor — "Not run" if no competitor export)
- Link magnet candidates flagged: [n] ([n] if none identified this session, say so plainly)

### AI Visibility Signals Applied
- Pages with FAQ schema: [n]
- Pages with Speakable schema: [n]
- Entity gaps flagged: [n]
- Featured snippet hooks written: [n] ([n] AI-citation formatted)
- Pages with a detected SERP feature matched structurally: [n] ([n] snippet, [n] PAA, [n] image pack, [n] shopping pack)
- llms.txt entries recommended: [n]

### Top 5 Priority Actions (ranked by Opportunity Score, not just tier)
1. [Most important T1 page/gap to build first]
2. [Second priority]
3. [Third priority]
4. [Fourth priority]
5. [Fifth priority]

### Documents Delivered
⚠️ All documents belong in docs/ only — never in public/ or the deploy ZIP (WebForge Rule 12).
- docs/keyword-map.md ✅
- docs/blog-plan.md ✅ (also the WebForge blog build queue — flip each post's Status to Built after it's published)
- docs/faq-bank.md ✅
- docs/product-gaps.md ✅

### Hand-off to WebForge
When starting a WebForge build session after running keyword-engine:
1. Attach docs/keyword-map.md and docs/blog-plan.md to the WebForge Claude Project
2. WebForge reads keyword-map.md for page meta, H1s, and on-page keyword targets
3. WebForge reads blog-plan.md for the blog post build queue (next unused post = next `Pending` row)
4. WebForge reads faq-bank.md for homepage FAQ and FAQ page content
5. WebForge reads product-gaps.md to decide which product/category pages to create
```

---

## MODE B Audit Output Format

Audit mode updates existing docs rather than creating new ones. The two files it modifies are keyword-map.md and blog-plan.md (the latter replaces the old keyword-cluster.txt target now that the two files are merged). Use these templates for the additions.

### keyword-map.md Audit Additions

Append the following sections to the END of the existing keyword-map.md. Never overwrite existing content — add below it with a clear audit header.

```markdown
---

## 🔍 Audit Results — [Date]
**Pages Crawled:** [n]
**Overall Health Score:** [X/100] — (PASS count / total pages checked × 100)

### Audit Status by Page

| URL | Planned Primary KW | Detected Primary KW | Secondaries Planned | Guarantee Flag Still Matches? | Audit Status | Issue | Fix Required |
|-----|--------------------|--------------------|---------------------|-------------------------------|--------------|----|------------|
| /url/ | [planned kw] | [detected kw] | 6/6 | Yes | ✅ PASS | — | — |
| /url/ | [planned kw] | **N/A — page is noindexed** | — | Yes | 🔴 CRITICAL | `noindex` directive present — every other check on this page is moot until this is fixed | Remove the `noindex` directive; re-check the rest of this row only after it's confirmed indexable |
| /url/ | [planned kw] | [different kw] | 5/5 | Yes | 🔴 CRITICAL | KW not in title or H1 | Update title tag and H1 to include "[planned kw]" |
| /url/ | [planned kw] | [planned kw] | 5/5 | Yes | 🟠 WARNING | KW missing from meta description | Add "[planned kw]" to meta description |
| /url/ | [planned kw] | [planned kw] | 3/5 ⚠️ | Yes | 🟠 WARNING | Planned secondaries under the 5+ floor (or 3+ for homepage/shop) — page mapped before this rule | Re-run secondary supplementation (filter-and-cluster.md), add 2 more secondaries |
| /url/ | [planned kw] | [different kw] | 5/5 | Yes | 🟡 DRIFTED | Page targeting wrong keyword | Either update plan or update page |
| /url/ | [planned kw] | [planned kw] | 5/5 | **No — Active-Conditional page no longer live** | 🟡 DRIFTED | Sale/Best Sellers/Compare/Wholesale trigger no longer applies | Update Guarantee Flag to reflect current state; don't leave it stale |

**Blog posts get a registry-only line here, not a full row** — their Status field already lives authoritatively in `blog-plan.md`; duplicating it into a second row here is exactly the two-files-same-data problem this skill's output documents already fixed once (the `keyword-cluster.txt`/`blog-plan.md` merge). Cross-reference against `blog-plan.md`'s own Status field for that post instead.

### ⚫ Cannibalisation Flags
| Keyword | Page A | Page B | Recommendation |
|---------|--------|--------|---------------|
| [keyword] | [url-a] | [url-b] | MERGE into [url] / DIFFERENTIATE: change [url-b] to target "[alt keyword]" |

Includes the homepage/shop near-duplicate check (flagged even without an exact keyword match — see `audit-mode.md` § Cannibalisation Severity) and every N-way carve-out (Sale's three-way, Best Sellers/New Arrivals' four-way, Wholesale's fourth-direction) at live-site scale, not just at plan time. Also includes the secondary-level (same secondary planned on two URLs in `keyword-map.md`) and FAQ-level (same buyer question answered on two or more crawled pages) checks — `audit-mode.md` § Secondary-level and FAQ-level cannibalisation — listed in this same table or as a short FAQ-duplicate note beneath it.

### 🟣 Orphan Pages
| URL | Guarantee-Mandated? | Discovered Via | Recommendation |
|-----|---------------------|---------------|---------------|
| [url] | Yes ([which Guarantee]) | [nav/link/sitemap] | **Relink per page-mapping.md's Internal Link Slots — never delete** |
| [url] | No | [nav/link/sitemap] | Assign cluster "[keyword]" / Consolidate into [url] / Delete + 301 to [url] |

### 💡 Bonus Opportunities
| Detected Signal | Found On | Suggested Cluster | Suggested Page | Potential |
|----------------|---------|-----------------|---------------|----------|
| [keyword signal] | [url] | [primary kw] + supplemented to 5+ | [existing url or new /slug/] | High / Medium |

### 🤖 AI/GEO Signal Gaps
| Page | Signal Missing | Severity | Fix |
|------|--------------|---------|-----|
| [url] | FAQ Schema | 🟠 WARNING | Add FAQPage JSON-LD — see faq-bank.md for questions |
| [url] | Definition hook | 🟡 DRIFTED | Add 1–2 sentence direct answer in first 150 words |

### 📊 Performance Validation (read live from GSC via the in-app browser by default; present unless neither live access nor a fallback export was available)
| URL | Planned Primary | Actual Top Query (GSC) | Status | Recommendation |
|-----|-----------------|------------------------|--------|-----------------|
| [url] | [planned kw] | [actual query] | 🔀 MISMATCH | Retarget / Reinforce |
| [url] | [planned kw] | [planned kw] | ✅ PASS | — |

**Striking Distance queue:** [n] queries at position 5–15 not yet targeted — see keyword-map.md § Performance Validation for the full table.
**Refresh queue:** [n] pages with 20%+ traffic drop — via live GSC Compare mode by default; skipped only if the fallback export had no trend column — see keyword-map.md § Performance Validation.
```

### blog-plan.md Audit Additions

Update each post's Status field inline (Pending → Built, as confirmed built during the crawl) rather than appending a separate log — this file's existing per-post rows/briefs are the single source of truth, not a parallel status list. For the 12-Week Content Calendar table specifically, flip the Status cell in place. Add any newly-discovered bonus topics as new full briefs in the Backlog Posts section (same Blog Brief Template as every other backlog entry, content-planning.md) — not a table row, since backlog posts here are full briefs, not calendar-table entries — each starting at Status: Pending and tagged with when the audit found it:

```
## Blog Brief: [Post Title] ← BONUS from [date] audit
[... full brief, same template as any other backlog post]
```

### Health Score Reference

| Score | Status | Meaning |
|-------|--------|---------|
| 90–100 | 🟢 Excellent | Nearly all pages correctly implementing keywords |
| 75–89 | 🟡 Good | Most pages correct, some warnings to fix |
| 60–74 | 🟠 Needs Work | Significant drift or missing implementations |
| 40–59 | 🔴 Poor | Major issues — priority fixes required before new content |
| Below 40 | 🔴 Poor — consider a full Mode A re-run | This many pages drifting this far usually means the original research itself no longer fits the site (taxonomy changed, catalog grew, business model shifted) — patching live pages one at a time won't close that gap. Recommend re-running Mode A from scratch rather than only working through the fix list. |

A site should aim for 85+ before focusing on new blog content. Critical issues always take priority over new page creation.

