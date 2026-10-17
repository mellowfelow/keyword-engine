# Output Format Templates

All five documents are produced at the end of every keyword engine session. They are designed to be read independently and used directly by code/build workflows.

---

## Document 1: keyword-map.md

```markdown
# Keyword Map — [Site Name] ([Market: US/UK])
**Generated:** [Date]
**Total Keywords Processed:** [n]
**Keywords Kept (Primary Pool):** [n]
**Keywords in Supporting Pool:** [n]
**Keywords Dropped:** [n]
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
- **Title Tag:** [formula output — max 60 chars]
- **H1:** [formula output]
- **Meta Description:** [formula output — 130–155 chars. This band satisfies both Google (≤160) and Bing (120–158). Target ~148 chars.]
- **Primary Keyword:** [keyword] (Opportunity Score: [n])
- **Secondary Keywords (5+ minimum — homepage: 3-5):** [kw1], [kw2], [kw3], [kw4], [kw5] [related-search], [kw6] [generated] — tag every supplemented keyword with its source (`[site-search]` / `[competitor]` / `[related-search]` / `[generated]`); untagged = export-backed real data
- **LSI/Supporting Keywords:** [list]
- **Image Alt Text:** [primary keyword — product detail]
- **Internal Links OUT:** [URL — anchor text], [URL — anchor text]
- **Internal Links IN:** [URL — where/how to link here]
- **FAQ Schema:** Yes / No
- **Speakable Target:** [CSS class e.g. `.faq-answer-speakable` / `.brand-statement`] / N/A — WebForge adds this class to the element during build
- **Entity Coverage:** ✅ Product | ✅ Brand | ✅ Category | ⚠️ Location missing
- **Definition Hook:** [1–2 sentence hook draft — place in first 150 words of page] — AI-citation formatted: fact-first, one claim per sentence, number anchored early
- **SERP Feature:** [Detected feature — Snippet (paragraph/list/table) / PAA / Image pack / Shopping pack / None] → [structural response applied — e.g. "comparison table added," "3 PAA questions folded into page FAQ"]
- **WebForge Schema Type:** Article / HowTo / FAQPage / Product / Review / Organization — tell WebForge which JSON-LD type this page needs beyond its defaults

[Repeat for every mapped page]

---

## Supporting Pool Keywords (KD 35–54)
These keywords are NOT primary targets. Use them to enrich copy on the pages listed — or as `[site-search]`/`[competitor]`/`[related-search]`/`[generated]` supplements to reach a cluster's 5+ secondary floor.

| Keyword | Vol | KD | Best Page to Use On | Role |
|---------|-----|-----|-------------------|------|
| [keyword] | [v] | [k] | [url] | LSI in body copy |

---

## Revisit in 6 Months (KD 35–54, Vol ≥ 2000)
| Keyword | Vol | KD | Notes |
|---------|-----|-----|-------|
| [keyword] | [v] | [k] | High demand, too competitive now — revisit when DA grows |

---

## Orphan Keywords (for manual review)
| Keyword | Vol | KD | Why Orphaned |
|---------|-----|-----|-------------|
| [keyword] | [v] | [k] | Single keyword, no cluster match |
```

---

## Document 2: blog-plan.md

```markdown
# Blog Plan — [Site Name] ([Market: US/UK])
**Generated:** [Date]
**Total Blog Posts Planned:** [n] — minimum 20 fully-briefed, delivered day one ([n] scheduled in the first 12-week window, [n] queued in the backlog beyond it)
**Pillar Posts:** [n]
**Standard Posts:** [n]
**20-Post Floor:** ✅ Met ([n] briefed) / ⚠️ Short ([n] briefed — see note on why genuine expansion couldn't reach 20)

---

## 12-Week Content Calendar (First Window — Backlog Continues Beyond Week 12)

| Week | Post Title | Primary Keyword | Type | Funnel | Tier | Words | WebForge Schema |
|------|-----------|----------------|------|--------|------|-------|----------------|
| 1 | [title] | [keyword] | [type] | Bottom | T1 | [n] | Article + FAQPage |
| 2 | [title] | [keyword] | [type] | Bottom | T1 | [n] | Article + HowTo |
[...]

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

All remaining briefed posts that didn't fit the first 12-week window — full briefs, same completeness as any scheduled post, ready to build whenever capacity allows. These are sequenced in keyword-cluster.txt alongside the scheduled posts, not held back for a future session.

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
A: [40–60 word answer. Concrete. Includes keyword. Ends with CTA or link.]

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
A: [50–80 word answer]

**Q: [Question]**
A: [50–80 word answer]

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

| Gap Name | Type | Demand Signal | CPC Signal | Priority | Est. Revenue Potential |
|----------|------|--------------|-----------|----------|----------------------|
| [name] | Brand | [combined vol] | High | T1 | High |
| [name] | Competitor | [combined vol] | Medium | T2 | Medium |
[...]

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

## Document 5: keyword-cluster.txt (WebForge companion file)

Always produce this alongside keyword-map.md. WebForge project instructions reference `docs/keyword-cluster.txt` directly — it reads this file to pull the next unused blog cluster for each new post build.

Format: flat text, one cluster per line, tab-separated. Mark each cluster as USED once WebForge builds that blog post.

```
# keyword-cluster.txt — [Site Name] ([Market])
# Generated by keyword-engine. Place in docs/. Never in public/.
# WebForge reads this to pick next unused blog cluster.
# Mark USED after WebForge builds each post.
# Minimum 20 fully-briefed clusters below — the 12-week window is a first pass, not a cap; backlog clusters beyond it are listed here too, ready to build.

[UNUSED]	electric dirt bikes for kids	/blog/electric-dirt-bikes-for-kids/	Informational	T1	1400w	Article+FAQPage
[UNUSED]	sur-ron vs segway x260	/blog/sur-ron-vs-segway-x260/	Commercial	T1	1800w	Article
[UNUSED]	how to charge an electric dirt bike	/blog/how-to-charge-electric-dirt-bike/	Informational	T2	1000w	Article+HowTo
[USED]	best electric dirt bikes 2025	/blog/best-electric-dirt-bikes/	Commercial	T1	2500w	Article
```

Column order: `[STATUS]` | Primary Keyword | Proposed URL | Intent | Tier | Word Count | WebForge Schema

---

## In-Chat Session Summary

At the end of every session, output this summary in chat before delivering the files:

```
## ✅ Keyword Engine — Session Complete

**Site:** [domain] ([market])
**Session Date:** [date]

### What Was Processed
- Raw keywords received: [n]
- Keywords kept (Primary Pool): [n]
- Keywords in Supporting Pool: [n]
- Keywords dropped: [n]

### What Was Built
- Keyword clusters created: [n]
- Existing pages mapped: [n]
- New pages needed: [n] (see product-gaps.md)
- Secondary-keyword floor: [n]/[n] pages at 5+ secondaries — [n] needed supplementation ([n] site-search, [n] competitor, [n] related-search, [n] generated), [n] shipped honestly under floor
- Programmatic page sets flagged: [n] (only if the catalog has genuine combinatorial scale — otherwise omit)
- Blog posts planned: [n] ([n] pillar, [n] standard) — 20-post floor: ✅ Met / ⚠️ Short ([n] scheduled in first 12 weeks, [n] in backlog)
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
- docs/keyword-cluster.txt ✅ (WebForge blog queue — mark clusters USED after each post build)
- docs/blog-plan.md ✅
- docs/faq-bank.md ✅
- docs/product-gaps.md ✅

### Hand-off to WebForge
When starting a WebForge build session after running keyword-engine:
1. Attach docs/keyword-map.md and docs/keyword-cluster.txt to the WebForge Claude Project
2. WebForge reads keyword-map.md for page meta, H1s, and on-page keyword targets
3. WebForge reads keyword-cluster.txt for the blog post build queue
4. WebForge reads faq-bank.md for homepage FAQ and FAQ page content
5. WebForge reads product-gaps.md to decide which product/category pages to create
```

---

## MODE B Audit Output Format

Audit mode updates existing docs rather than creating new ones. The two files it modifies are keyword-map.md and keyword-cluster.txt. Use these templates for the additions.

### keyword-map.md Audit Additions

Append the following sections to the END of the existing keyword-map.md. Never overwrite existing content — add below it with a clear audit header.

```markdown
---

## 🔍 Audit Results — [Date]
**Pages Crawled:** [n]
**Overall Health Score:** [X/100] — (PASS count / total pages checked × 100)

### Audit Status by Page

| URL | Planned Primary KW | Detected Primary KW | Secondaries Planned | Audit Status | Issue | Fix Required |
|-----|--------------------|--------------------|---------------------|--------------|----|------------|
| /url/ | [planned kw] | [detected kw] | 6/6 | ✅ PASS | — | — |
| /url/ | [planned kw] | [different kw] | 5/5 | 🔴 CRITICAL | KW not in title or H1 | Update title tag and H1 to include "[planned kw]" |
| /url/ | [planned kw] | [planned kw] | 5/5 | 🟠 WARNING | KW missing from meta description | Add "[planned kw]" to meta description |
| /url/ | [planned kw] | [planned kw] | 3/5 ⚠️ | 🟠 WARNING | Planned secondaries under the 5+ floor — page mapped before this rule | Re-run through Phase 4/5 supplementation, add 2 more secondaries |
| /url/ | [planned kw] | [different kw] | 5/5 | 🟡 DRIFTED | Page targeting wrong keyword | Either update plan or update page |

### ⚫ Cannibalisation Flags
| Keyword | Page A | Page B | Recommendation |
|---------|--------|--------|---------------|
| [keyword] | [url-a] | [url-b] | MERGE into [url] / DIFFERENTIATE: change [url-b] to target "[alt keyword]" |

### 🟣 Orphan Pages
| URL | Discovered Via | Recommendation |
|-----|---------------|---------------|
| [url] | [nav/link/sitemap] | Assign cluster "[keyword]" / Consolidate into [url] / Delete + 301 to [url] |

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

### keyword-cluster.txt Audit Additions

Update status flags inline, add new bonus clusters at bottom:

```
# Last audited: [date] — [n] clusters confirmed USED, [n] bonus clusters added

[USED]    [primary keyword]    [url]    [intent]    [tier]    [wordcount]    [schema]
[UNUSED]  [primary keyword]    [url]    [intent]    [tier]    [wordcount]    [schema]    ← BONUS from [date] audit
```

### Health Score Reference

| Score | Status | Meaning |
|-------|--------|---------|
| 90–100 | 🟢 Excellent | Nearly all pages correctly implementing keywords |
| 75–89 | 🟡 Good | Most pages correct, some warnings to fix |
| 60–74 | 🟠 Needs Work | Significant drift or missing implementations |
| Below 60 | 🔴 Poor | Major issues — priority fixes required before new content |

A site should aim for 85+ before focusing on new blog content. Critical issues always take priority over new page creation.

