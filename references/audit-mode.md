# Audit Mode Reference (MODE B)

## What Audit Mode Does

Crawls a live site using only its URL. Extracts the actual keyword signals present on every page — titles, H1s, meta descriptions, body copy, schema, FAQ content. Compares what's live against what was planned. Updates the strategy docs to reflect the current state, flag drift, surface cannibalisation, find orphan pages, track blog progress, and spot new keyword opportunities the original plan missed.

**No keyword paste. No existing docs required.** The skill reverse-engineers the full keyword picture from the live site alone.

---

## Audit Severity Levels

Apply consistently across all audit phases. Every finding gets exactly one severity tag.

| Tag | Severity | Meaning | Action Required |
|-----|----------|---------|----------------|
| 🔴 CRITICAL | Highest | Primary keyword missing from BOTH title tag AND H1 | Fix immediately — this page is not ranking for its target keyword |
| 🟠 WARNING | High | Primary keyword present on page but missing from meta description OR not in first 100 words | Fix soon — partial implementation limits ranking potential |
| 🟡 DRIFTED | Medium | Keyword is present but in wrong position, wrong density, or displaced by a competing term | Fix in next update cycle |
| ⚫ CANNIBAL | Critical | Two or more pages competing for the same primary keyword | Merge or differentiate — splits authority and hurts both pages |
| 🟣 ORPHAN | Medium | Page exists on the live site with no keyword assignment and no clear SEO direction | Assign a keyword cluster or consolidate into another page |
| 🔵 PENDING | Info | Blog post in blog-plan.md still marked Status: Pending — not yet built | Schedule for next content sprint |
| ✅ PASS | Good | Primary keyword correctly implemented in all required positions | No action needed |
| 💡 BONUS | Opportunity | New keyword signal spotted on site not in original plan — potential cluster to add | Add to keyword-map.md (page topic) or blog-plan.md (blog topic, Status: Pending) |
| 📉 DECAY | High | Page's clicks/impressions dropped materially vs the previous period, per GSC's Compare mode (live) or a trend column (fallback export) | Route to Refresh Queue — content update, not a new page |
| 🎯 STRIKING DISTANCE | Opportunity | Query already getting impressions at position 5–15 but isn't a planned secondary | Add as secondary or strengthen on-page signal — this is the cheapest ranking gain available |
| 🔀 MISMATCH | High | Page is planned for keyword A but GSC data (live read or fallback export) shows it actually earning impressions for keyword B | Reassess: retarget the page to B, or reinforce A's on-page signal if B is a false read |

---

## AUDIT PHASE 1 — Site Crawl & Keyword Extraction

### Crawl Protocol

1. **Fetch homepage** via web_fetch — extract: title tag, meta description, H1, first 200 words of body copy, FAQ questions, schema types present, navigation links
2. **Extract all internal links** from homepage navigation and footer — build page inventory
3. **Fetch each inner page** — extract same fields: title, meta, H1, first 200 words, any FAQ content, schema type
4. **Prioritise crawl order:** homepage → shop page → category pages → product pages → Brand Hub/individual Brand pages → blog posts → FAQ page → Sale/Best Sellers/New Arrivals/Compare/Wholesale (whichever are actually live) → utility pages. This mirrors `page-mapping.md`'s own Mapping Priority Order (product and category/brand pages rank above blog posts there too) — the crawl shouldn't invert the priority the research phase itself used. Every one of these gets its own page-type identity in the crawl — none of them fall into an undifferentiated "other," since each carries its own rules (e.g. Best Sellers' four-way cannibalisation check, Brand Hub's 3+-brand trigger) that a generic bucket would miss.
5. **Cap at 40 pages** per audit session. For larger sites, crawl the most important pages first (homepage, shop page, top categories, top products by URL position depth), note how many were skipped.

### What to Extract Per Page

For every page crawled, record:

```
URL: [full URL]
Page Type: Homepage / Shop / Category / Subcategory / Product / Brand Hub / Individual Brand / Sale / Best Sellers / New Arrivals / Compare / Wholesale / Blog / Blog Index / FAQ Page / Utility-Tier1
Title Tag: [extracted — note if truncated >60 chars]
Meta Description: [extracted — note if outside 130–155 chars]
H1: [extracted — note if missing or multiple H1s found]
First 100 Words: [extracted]
Keywords Detected: [list of keyword signals visible in title+H1+meta+body]
Schema Types Found: [Article / Product / FAQPage / Organization / etc]
FAQ Questions Found: [list if any]
Internal Links Out: [count + sample destinations]
Indexability: [meta robots content attribute, if present — "index,follow" / "noindex,..." / not present (defaults to indexable)]
```

### Keyword Detection Method

Extract keyword signals by scanning for:
- Exact phrases in title, H1, meta (strongest signal)
- Exact phrases in first 100 words (strong signal)
- Exact phrases in H2/H3 headings (medium signal)
- Exact phrases in body copy (supporting signal)
- Terms present in schema `name`, `description`, `keywords` fields (schema signal)

Build a **Detected Keyword Map** — a table of every page and its apparent primary keyword (the most prominent phrase in title+H1), plus secondary keywords visible in the page.

---

## AUDIT PHASE 2 — Implementation Check

### If keyword-map.md is available (pasted or in context)

Compare the Detected Keyword Map from Phase 1 against the planned assignments in keyword-map.md.

For each planned page assignment, check:

| Check | Pass Condition | Fail = Severity |
|-------|---------------|----------------|
| Page is indexable — check this first, before anything else | No `noindex` directive on a page that's supposed to rank — **every page with an entry in keyword-map.md, regardless of its Guarantee Flag value** (Yes, No/pre-existing, or Active-Conditional — a pre-existing mapped page is just as meant to rank as a Guarantee-built one) | 🔴 CRITICAL — this makes every other check on this page moot. A perfect title/H1/meta/secondary setup on a noindexed page will never rank; flag and fix this before evaluating anything else about the page |
| Primary keyword in title tag | Exact match or close variant in first 4 words | 🔴 CRITICAL if missing |
| Primary keyword in H1 | Exact match or close variant | 🔴 CRITICAL if missing |
| Primary keyword in meta description | Present anywhere in meta | 🟠 WARNING if missing |
| Primary keyword in first 100 words | Present at least once | 🟠 WARNING if missing |
| Secondary keywords present | At least 3 of the planned secondaries (5–8) appear somewhere on page | 🟡 DRIFTED if fewer than 3 |
| Planned secondary count meets the floor | keyword-map.md shows 5+ secondaries planned for this page (homepage and shop page: 3+) | 🟠 WARNING if the *plan itself* is under floor — this page was mapped before the 5+ rule and needs re-running through Phase 4/5 supplementation, not just a content fix |
| Title tag length | 60 chars or under | 🟡 DRIFTED if over |
| Meta description length | 130–155 chars | 🟡 DRIFTED if outside band |
| One H1 only | Exactly one H1 tag | 🟠 WARNING if multiple |
| Definition hook present | A 1–2 sentence direct answer in first 150 words | 🟡 DRIFTED if missing |
| Guarantee Flag still matches reality | A page marked Active-Conditional in keyword-map.md (Sale/Best Sellers/New Arrivals/Compare/Wholesale) is actually still live and findable on the site; a page the plan marks No-longer-active isn't still live with stale content | 🟡 DRIFTED if a conditional page's live status has silently diverged from its planned Guarantee Flag — flag for Layer 2-style re-classification, not a content fix |
| New Arrivals year-stamped primary still current | A New Arrivals primary naming a specific year (e.g. "new electric dirt bikes 2026") still matches the current year | 🟡 DRIFTED if the year has rolled over and the primary wasn't updated — route to re-pick the primary with the current year, not a content-only fix |
| Wholesale secondaries are genuinely B2B-flavored | Wholesale page's secondaries include bulk/trade/account-style terms, not just the retail cluster's ordinary secondaries reused as-is | 🟠 WARNING if Wholesale's secondaries read identically to a retail category page's |
| KD ceiling still honored on the live primary (optional — only if a refreshed Semrush/platform link is provided this audit session) | The detected primary keyword's KD, re-checked live via the link, is still ≤28 — a keyword can drift in difficulty over time the same way rankings do | 🟡 DRIFTED if the live primary now sits above 28; route to re-pick a primary, not a content tweak. **Skip this check entirely if no link was provided** — Mode B's baseline input is the site URL alone, not a live KD re-check; don't assume or estimate KD without the actual data. |

### If no keyword-map.md is available

Skip the comparison step. Work entirely from the Detected Keyword Map built in Phase 1. Flag pages where:
- A `noindex` directive is present on a page that otherwise looks like it's meant to rank (has real content, internal links, a clear keyword focus) → 🔴 CRITICAL — check this first, same priority as the plan-comparison branch above
- No clear primary keyword is detectable (title and H1 are vague or generic) → 🔴 CRITICAL
- Title and H1 use different primary keywords → 🟠 WARNING
- Meta description doesn't match the title/H1 keyword signal → 🟠 WARNING
- Page appears thin (under 300 words detected) → 🟡 DRIFTED

At end of Phase 2 without a plan doc, also produce a **Reverse-Engineered Keyword Map** — the skill's best read of what keyword each page is currently targeting, to serve as the new baseline.

---

## AUDIT PHASE 3 — Cannibalisation Scan

### Detection Method

After Phase 1 crawl, group all detected primary keywords across pages. Flag any keyword (or near-variant) that appears as the apparent primary on more than one page.

**Near-variant rule:** treat these as the same keyword for cannibalisation purposes:
- Singular vs plural ("electric dirt bike" / "electric dirt bikes")
- Word order variants ("kids electric dirt bike" / "electric dirt bike for kids")
- Minor modifier differences ("best electric dirt bike" / "top electric dirt bike") — same intent, same SERP

### Cannibalisation Severity

| Type | Example | Severity |
|------|---------|----------|
| Exact match on two pages | Two product pages both targeting "Sur-Ron Light Bee X" | ⚫ CANNIBAL — Critical |
| Near-variant across page types | Category page + blog post both targeting "electric dirt bikes for kids" | ⚫ CANNIBAL — Critical |
| Partial overlap (same secondary keyword as primary on another page) | Secondary "youth electric bike" on category + primary on a product page | 🟡 DRIFTED — monitor |
| Homepage/shop near-duplicate | Homepage and shop page primaries aren't exact matches but read as substantively the same page (same framing, no real catalog-entry vs. brand distinction) | ⚫ CANNIBAL — these are the site's two highest-authority pages; a near-duplicate pair wastes both, flag it even without an exact keyword match |

### Secondary-level and FAQ-level cannibalisation (the other two levels of `page-mapping.md`'s build-time Cannibalisation Audit — checked live here too, not just at plan time)

**Secondary-level (when `keyword-map.md` is available):** scan the Per-Page secondary keyword lists across every planned page for the same secondary assigned to two different URLs — this is a document-level check against the plan, not a crawl-detection one. Flag as 🟡 DRIFTED (same severity as the Partial Overlap row above, since the mechanism is the same: a keyword splitting relevance across two pages).

**FAQ-level (from Phase 1's "FAQ Questions Found" field, always available):** group every FAQ question detected across the crawl — homepage FAQ, dedicated FAQ page, and every page-level mini-FAQ — and flag any question (or near-variant, same rule as keyword near-variants above) answered on two or more pages. This mirrors `page-mapping.md`'s FAQ-level build-time check: the same buyer question should be answered on exactly one page, with every other page linking to it instead of duplicating the Q&A. Severity: 🟡 DRIFTED.

```
🟡 DRIFTED — FAQ duplicate: "[question or near-variant]"
  Page A: [URL]   Page B: [URL]
  Recommendation: keep the answer on the best-fit page, replace the other with a link to it
```

### Merge Recommendation Logic

When cannibalisation is found, assess whether pages are close enough to merge:

**Recommend MERGE if:**
- Both pages cover the same product/topic at the same depth
- One page has significantly lower traffic potential (shorter, thinner, fewer keywords)
- The pages are the same page type (two blog posts, two category pages)
- Combining them would produce a stronger, more comprehensive page

**Recommend DIFFERENTIATE if:**
- Pages serve different intents (one transactional, one informational)
- Pages target meaningfully different audience segments
- Both pages have substantial unique content worth keeping

**Output per cannibalisation flag:**
```
⚫ CANNIBAL: "[keyword]"
  Page A: [URL] — [page type] — [why it should/shouldn't own the keyword]
  Page B: [URL] — [page type] — [why it should/shouldn't own the keyword]
  Recommendation: MERGE into [URL] / DIFFERENTIATE by [how]
  If merging: redirect [losing URL] → [winning URL] (301)
  If differentiating: change [Page B] primary keyword to [alternative keyword]
```

---

## AUDIT PHASE 4 — Orphan Page Detection

### Detection Method

During the Phase 1 crawl, every page discovered is logged. After the crawl:
1. List all discovered URLs
2. Cross-reference against keyword-map.md planned assignments (if available)
3. Any discovered URL with NO keyword assignment = orphan candidate

### Orphan Classification

**Before recommending delete/consolidate on anything: check whether the page is Guarantee-mandated first.** A real taxonomy category/subcategory, a product in the stock list, the FAQ page, or a brand page for a brand the site actually stocks is *supposed* to exist regardless of its current link health — a Guaranteed page that lost its internal links is a linking bug to fix (relink it), never a deletion candidate. Only a genuinely non-Guaranteed page (a one-off blog post, an old campaign page, a conditional page whose trigger no longer applies) is eligible for delete/consolidate.

| Type | Description | Action |
|------|-------------|--------|
| True orphan — Guarantee-mandated | Page exists, no internal links pointing to it, no keyword assignment — but it's a category/product/FAQ/stocked-brand page that must exist per its Guarantee | 🟣 ORPHAN — **relink it, never delete.** Re-run its Internal Link Slots requirement (`page-mapping.md` § On-Page Requirements Per Mapped Page) to restore the links it should have had |
| True orphan — not Guarantee-mandated | Page exists, no internal links pointing to it, no keyword assignment, and nothing requires it to exist | 🟣 ORPHAN — assign a keyword cluster, or delete + 301 if it has no real purpose |
| Unassigned page | Page has internal links but no keyword assignment in the plan | 🟣 ORPHAN — assign a keyword cluster |
| Thin page | Page exists and is linked but has under 300 words and no clear keyword | 🟣 ORPHAN — expand with keyword content or consolidate |
| Legacy page | Page appears to be old/outdated content with no current keyword relevance | 🟣 ORPHAN — redirect to relevant current page or noindex |

**Output per orphan:**
```
🟣 ORPHAN: [URL]
  Discovered via: [how found — nav link / internal link / sitemap]
  Guarantee-mandated: Yes ([which Guarantee — category/product/FAQ/stocked-brand]) / No
  Content summary: [1 sentence on what the page contains]
  Recommendation: Relink per page-mapping.md's Internal Link Slots (if Guarantee-mandated) / Assign keyword cluster "[cluster]" / Consolidate into [URL] / Delete + redirect to [URL] (only if not Guarantee-mandated)
```

---

## AUDIT PHASE 5 — Blog Post Status Check

### If blog-plan.md is available

Read the `Pending` / `Built` Status field of every post row/brief (the 12-Week Content Calendar table and the Backlog Posts section both carry this field — there is no separate `keyword-cluster.txt` file to check instead). For each `Pending` post, check whether a blog post for that topic now exists on the live site (the build may have happened but the field was never flipped).

**Match logic:** a post is considered Built if a crawled blog URL contains the primary keyword in its slug, title, or H1.

Update status accordingly:
- Found on site → change that post's Status from `Pending` to `Built`, in place, in `blog-plan.md` (12-Week table row or backlog brief, whichever it is) — this is an inline field update, not a separate file to keep in sync
- Not found on site → keep `Pending`, flag in audit summary as pending

### If no blog-plan.md is available

Crawl all blog posts found on the site. For each post, extract:
- Primary keyword (from title/H1)
- Approximate topic cluster
- Whether it has a FAQ section
- Schema type implemented

Build a **Blog Inventory** showing what's live and what gaps remain based on the niche. This also becomes the seed for a fresh `blog-plan.md` if the client wants one rebuilt — every detected post starts at Status: `Built` (it's already live), and the Reverse-Engineered Keyword Map from Phase 2 feeds its Keywords section.

### Blog Health Checks (run on every crawled post)

| Check | Pass | Flag |
|-------|------|------|
| Primary keyword in slug | Yes | 🟡 DRIFTED if not |
| Primary keyword in title and H1 | Yes | 🔴 CRITICAL if missing from both |
| Post has FAQ section | Yes | 🟡 DRIFTED if missing |
| Post has internal links to product/category pages | Min 2 | 🟠 WARNING if fewer |
| Post has internal links from other posts/pages | At least 1 | 🟣 ORPHAN if none |
| Schema type implemented | Article minimum | 🟠 WARNING if missing |
| "Last updated" date present | Yes | 🟡 DRIFTED if missing (freshness signal) |

---

## AUDIT PHASE 6 — Strategy Gap Analysis

### New Keyword Opportunities

While crawling the site, look for keyword signals that appear in the content but were NOT part of the original keyword plan (or don't exist in keyword-map.md). These are 💡 BONUS opportunities.

**Sources of bonus opportunities:**
- Product names/specs visible on pages that weren't in the original keyword batch
- FAQ questions on the site that map to high-value search queries
- Brand names mentioned in product descriptions that could become clusters
- Location signals in copy that could trigger local keyword opportunities
- Accessory/part names in product descriptions that could become accessory keyword clusters

**For each bonus opportunity:**
```
💡 BONUS: "[detected keyword signal]"
  Found on: [URL]
  Context: [where/how it appears]
  Suggested cluster: [proposed primary keyword] — run through Secondary Keyword Supplementation (filter-and-cluster.md) to reach 5+ before adding to keyword-map.md; don't add a bonus cluster under floor
  Suggested page: [existing page to strengthen / new page to create]
  Estimated potential: High / Medium / Low (based on specificity and commercial intent)
```

### Coverage Gaps

Compare the niche against what's covered. Flag any major topic in the niche that has NO page and NO planned cluster:
- Major product categories with no page
- Key brand names in the niche with no brand page (and a Brand Hub missing once 3+ brands are actually stocked)
- Common buyer questions with no FAQ answer
- Comparison topics (X vs Y) with no blog post, and no Compare page if the site's nav/structure suggests one should exist
- **Conditional pages the business model now supports but the site doesn't have**: sale/promo inventory visible on-site with no Sale page, sales-ranking or new-arrivals data implied by nav/content with no Best Sellers/New Arrivals page, a bulk/wholesale offering mentioned anywhere with no Wholesale page — these are 💡 BONUS-tier findings (a real opportunity, not a defect), flagged the same way as any other coverage gap
- **Blog launch batch floor**: judge the site's niche tier from its catalog/category breadth the same way `content-planning.md` § Launch Batch Floor does (Micro/Small <50 products or 1–3 categories → 25–30; up to Massive 1000+ products → 100+), then cross-reference the site's actual blog post count against that tier's target — a site well short of its tier's target is a real strategy gap worth surfacing, not just a Phase 5 status question. **If the catalog breadth itself can't be judged from the crawl, skip this specific check rather than guessing a target** — flag the raw post count as context instead.

---

## AUDIT PHASE 7 — AI/GEO Signal Check

Run these checks on the crawled pages. Flag missing signals.

| Signal | Check | Severity if Missing |
|--------|-------|-------------------|
| FAQ Schema | FAQPage JSON-LD present on FAQ page and homepage | 🟠 WARNING |
| Page-Level FAQ | For any page whose `keyword-map.md` row has FAQ Schema = Yes, a 2–4 question mini-FAQ with its own FAQPage schema is actually live on that page (not just planned) — `content-planning.md` § Page-Level FAQ | 🟡 DRIFTED |
| Speakable Schema | `.brand-statement` or `.faq-answer-speakable` class present on homepage | 🟡 DRIFTED |
| Brand entity statement | Clear 1–2 sentence brand description in first 200 chars of homepage body | 🟠 WARNING |
| Definition hooks | 1–2 sentence direct answer in first 150 words of blog posts | 🟡 DRIFTED |
| Organization schema | Present on homepage with `knowsAbout`, `areaServed`, `sameAs` fields; `knowsAbout[]` reflects terms from **both** the homepage's and the shop page's primary+secondary keywords, not homepage-only | 🟠 WARNING (missing fields) / 🟡 DRIFTED (knowsAbout present but shop-page terms missing from it) |
| Entity coverage | Product, brand, category entities named on each page | 🟡 DRIFTED if vague |
| Freshness signals | `dateModified` in Article schema + "Last updated" text on posts | 🟡 DRIFTED |
| llms.txt present | File exists and includes top-priority pages | 🟠 WARNING if missing |

---

## AUDIT PHASE 8 — Performance Validation (Live GSC via In-App Browser)

**Primary method: live browser access, not a manual export.** The user stays logged into Google Search Console in the in-app browser. Use that session directly — navigate to Search Console and read the Performance report for the site being audited, the same way the skill already uses `web_fetch`/browser access to crawl the live site in Phase 1. Don't ask the user for a CSV paste unless Step 0 below fails.

**Why this phase exists:** Phases 1–7 check whether the *plan was implemented* (keyword present in title/H1/meta). None of them check whether the plan is actually *working* — whether the planned primary keyword is the one Google is actually showing the page for, and whether any page's traffic is trending down. This phase closes that loop using real ranking data instead of assumptions.

### Step 0 — Access Search Console

1. Open `https://search.google.com/search-console` in the in-app browser (the user's session is already authenticated there).
2. Match the site being audited to a property in the account by domain. If more than one property matches (e.g. both a domain property and a URL-prefix property for the same site), prefer the one with the fuller data history.
3. **If the property isn't found in the logged-in account, or the browser isn't available/authenticated this session** → fall back to asking for a manual export instead (Search Console → Performance → export the Queries and Pages tables as CSV, Query/Page/Clicks/Impressions/CTR/Position columns). Same processing applies to a pasted export as to live-read data in every step below. If neither live access nor an export is available, skip Phase 8 entirely and say so plainly in the audit summary — never block the rest of the audit on it.

### Step 1 — Pull Queries and Pages data

Once on the property's Performance report:
1. Set the date range to the default comparison window (GSC's own "Last 3 months," or whatever range is already active) and turn on **Compare → Compare to previous period** using the UI's own date-range control. This gives period-over-period % change columns directly in the report — no need for the user to run two separate exports.
2. Read the **Queries** tab (via `get_page_text`/`read_page` on the rendered table) — capture Query, Clicks, Impressions, CTR, Position, and the % change column from Compare mode.
3. Read the **Pages** tab the same way — capture Page, Clicks, Impressions, CTR, Position, % change.
4. For per-page query attribution (needed for Step 3's Mismatch Check): filter the Queries tab by a specific page — GSC supports clicking into a page row or applying a Page filter — so the top queries pulled are genuinely the ones driving that specific URL, not just the site's overall top queries.

### Step 2 — Match GSC pages to keyword-map.md

For every URL read from the Pages report, find its planned entry in keyword-map.md (or the Reverse-Engineered Keyword Map from Phase 2 if no plan doc exists).

### Step 3 — Mismatch Check

For each matched page, look at its top queries by impressions (from the per-page filtered view in Step 1.4).

- **If the planned primary keyword (or a close variant) is the top or near-top query by impressions** → ✅ PASS, the plan is working as intended.
- **If a different query is earning meaningfully more impressions than the planned primary** → 🔀 MISMATCH. Two ways to resolve, call it explicitly rather than defaulting to one:
  - **Retarget** — if the actual query is commercially equal or better (similar/higher volume, same buyer intent), recommend making it the new primary and demoting the old one to secondary.
  - **Reinforce** — if the planned primary is still the right commercial target but simply isn't ranking yet, recommend strengthening its on-page signal (title/H1/first-100-words) rather than abandoning it.

### Step 4 — Striking Distance Opportunities

Scan every query sitting at **position 5–15 with non-trivial impressions** (use judgment on the threshold relative to the site's overall volume — a query with 500 impressions/month at position 8 is a real opportunity, one with 5 impressions is noise).

For each one not already a planned primary or secondary on that page:
- Flag 🎯 STRIKING DISTANCE
- These are the cheapest wins available — the query is already showing the page, it just needs a stronger signal (add to title/H1/secondary list, strengthen the page-level FAQ, add internal links) rather than needing new content built from scratch
- Recommend adding it to the page's secondary keyword list if it fits the cluster's intent; if it doesn't fit any existing page well, flag it as a 💡 BONUS cluster candidate instead (Phase 6)

### Step 5 — Decay Check

With Compare mode active (Step 1.1), every query and page row already carries its own period-over-period % change — no separate export or snapshot comparison needed.

- Flag any page where clicks or impressions dropped **20%+ over the comparison period** as 📉 DECAY
- Route decayed pages to a **Refresh Queue** — these need a content update (fresh examples, updated specs/pricing, expanded sections, a new FAQ entry, an updated "Last updated" date), not a brand-new page and not a keyword change unless Step 3's Mismatch Check also flagged the same page
- Rank the Refresh Queue by combined lost clicks (highest first) so the biggest bleeds get fixed first
- **If a manual single export was used instead of live Compare mode (Step 0 fallback) and it carries no trend/comparison column:** skip this step and note in the audit summary that decay wasn't checked — a single snapshot can't show a trend. This is now the exception, not the default, since live browser access gets Compare mode for free.

### Output

```
## 📊 Performance Validation — [Date, live GSC read or export date]

**Data source:** Live GSC via in-app browser / Manual CSV export (fallback) — state which
**Pages matched to GSC data:** [n] of [n] planned pages
**Mismatches found:** [n]
**Striking Distance opportunities:** [n]
**Decayed pages:** [n] (skipped only if fallback export had no trend data)

### 🔀 Mismatches
| URL | Planned Primary | Actual Top Query (GSC) | Impressions | Recommendation |
|-----|-----------------|------------------------|-------------|-----------------|
| /url/ | [planned kw] | [actual query] | [n] | Retarget to actual query / Reinforce planned primary |

### 🎯 Striking Distance (Position 5–15)
| Query | Page | Position | Impressions | Recommendation |
|-------|------|----------|-------------|-----------------|
| [query] | /url/ | 8 | [n] | Add as secondary + strengthen on-page signal |

### 📉 Refresh Queue (ranked by lost clicks)
| URL | Click Change | Likely Cause | Recommended Fix |
|-----|-------------|-------------|-----------------|
| /url/ | -35% | Content aged, competitor refreshed theirs | Update specs/pricing, add new FAQ entry, refresh "Last updated" date |
```

Append this section to keyword-map.md under a `## Performance Validation` header, same pattern as the other audit sections. Add any new Striking Distance keywords to the relevant page's secondary list in the main allocation table (respecting the existing 5+ floor — or 3+ if the page is the homepage or shop page — and cannibalisation registry; a Striking Distance keyword is still subject to the same "not already used elsewhere" check as any other secondary).

---

## Audit Output — What Gets Updated

**Exact templates for both updated files live in `output-formats.md` § MODE B Audit Output Format — not restated here, to avoid the same two-files-same-data problem this skill's output documents already had to fix once (the `keyword-cluster.txt`/`blog-plan.md` merge).** In short: `keyword-map.md` gets an Audit Status column added to its allocation table plus appended Cannibalisation/Orphan/Bonus/Metadata sections (blog posts get a registry-only line, never a full row); `blog-plan.md` gets each confirmed-built post's Status flipped `Pending` → `Built` in place, with new bonus topics added as full Backlog briefs. Run the phases above, then apply those exact templates.

### In-Chat Audit Summary

Output this in chat immediately after completing all audit phases:

```
## 🔍 Keyword Engine — Audit Complete

**Site:** [domain] ([market])
**Audit Mode:** Plan-comparison (keyword-map.md/blog-plan.md provided) / Full reverse-engineering (no docs — baseline built from the live crawl alone) — state which, since it changes how much the findings below can be trusted against an actual plan versus the skill's own best read of the site
**Audit Date:** [date]
**Pages Crawled:** [n] of [n total estimated]

---

### Health Score: [X/100]
Calculated as: (PASS pages / total pages checked) × 100

### Findings by Severity
🔴 CRITICAL: [n] pages — primary keyword missing from title AND H1
🟠 WARNING: [n] pages — keyword missing from meta or first 100 words
🟡 DRIFTED: [n] pages — keyword present but not correctly positioned
⚫ CANNIBAL: [n] keyword conflicts found
🟣 ORPHAN: [n] pages with no keyword assignment ([n] Guarantee-mandated and relinked, [n] genuinely orphaned)
🔵 PENDING: [n] blog posts in blog-plan.md still Pending, not yet built
💡 BONUS: [n] new keyword opportunities spotted ([n] page-level, [n] blog)

### Performance Validation (read live from GSC via in-app browser by default; falls back to a manual export only if live access fails — otherwise state "Not run — no GSC access or export available")
🔀 MISMATCH: [n] pages ranking for a different query than planned
🎯 STRIKING DISTANCE: [n] queries at position 5–15 not yet targeted
📉 DECAY: [n] pages with 20%+ drop (only if trend data available)

---

### Critical Fixes (do these first)
[List all 🔴 CRITICAL items with URL and specific fix]

### Cannibalisation Resolutions
[List all ⚫ CANNIBAL items with merge/differentiate recommendation]

### Top Bonus Opportunities
[List top 3–5 💡 BONUS items by potential]

### Performance Wins (only if Phase 8 ran — live GSC read or fallback export)
[List top 3–5 🎯 STRIKING DISTANCE opportunities and any 🔀 MISMATCH pages — these are usually the cheapest ranking gains in the whole audit since the query is already showing the page]

---

### docs/ Files Updated
- docs/keyword-map.md ✅ — audit status column added, [n] new findings appended[, Performance Validation section added]
- docs/blog-plan.md ✅ — [n] posts flipped Pending → Built, [n] bonus posts added to Backlog

### Recommended Next Actions
1. [Highest priority fix — if Health Score is below 40, this should be "Re-run Mode A from scratch" per output-formats.md § Health Score Reference, not an incremental fix]
2. [Second priority]
3. [Third priority]
4. [Fourth priority]
5. [Fifth priority]
```

---

## Mode B's own dedicated audit layer

Governed by Rule 5 (`core-rules.md`). Every deliverable this skill produces gets checked before it ships, then re-checked when the rules it depends on change — Mode B is no exception, and this section is where that discipline lives for it, consolidated here rather than scattered across the phases above.

**What this layer checks is different from what Mode B itself reports.** Mode B's findings (CRITICAL/WARNING/orphans/etc.) are diagnostic output *about the live site* — a site full of findings isn't a failure of Mode B, that's the audit working. This layer checks whether **Mode B's own execution was correct**: did it actually run its phases as designed, not whether the site it audited happens to be clean.

**Pre-ship checklist (run at the end of every Mode B session, before the audit output is delivered):**
1. **Crawl discipline** — the 40-page cap was respected, and the priority order actually followed `page-mapping.md`'s own Mapping Priority Order (product/category/brand above blog posts), not an arbitrary crawl sequence. Every page type got its own identity in the Page Type field — none were lumped into a generic bucket that should have had its own category. Indexability (meta robots) was actually captured per page, not skipped as a minor field.
2. **Indexability was checked first, on every page, before any other verdict was reached about it.** A `noindex` finding is 🔴 CRITICAL and makes every other check on that page moot — confirm this ran as the first check, in both the plan-comparison and reverse-engineering branches of Phase 2, not added as an afterthought to a page already marked PASS on other grounds.
3. **Severity tagging was applied to the defined table, not invented ad hoc.** 🔴 CRITICAL only where both title AND H1 are genuinely missing the primary keyword (or a `noindex` directive is present), not just one; every other tag matches its defined condition, not a looser judgment call.
4. **Guarantee-check-before-delete discipline actually ran, for every single orphan finding, no exceptions.** No delete/consolidate recommendation went out without first checking whether the page is Guarantee-mandated (a real taxonomy category/subcategory, a stocked product, the FAQ page, a stocked brand — `page-mapping.md` § 7's carve-out list) — this is the one check in this whole layer most worth re-verifying, since getting it wrong means recommending a destructive action against a page that's supposed to exist.
5. **Homepage/shop treatment used the 3+ floor, not the ordinary 5+**, when checking those two specific pages — and their near-duplicate check ran even when no exact keyword matched.
6. **Optional-data checks were actually skipped when their data wasn't provided, not guessed around.** The KD-recheck (Phase 2) and the launch-batch-floor check (Phase 6) only ran if a Semrush link / niche tier was genuinely available this session — neither was estimated or assumed in its absence.
7. **`blog-plan.md`'s Status field was read and flipped correctly** — `Pending` → `Built` only on genuine on-site confirmation, never flipped speculatively, and new bonus posts added as full Backlog briefs (Status: `Pending`), never as a bare table row.
8. **Both output files used the canonical templates** (`output-formats.md` § MODE B Audit Output Format) — not a locally-improvised format that drifted from the one source of truth.
9. **No `keyword-cluster.txt` reference or `[UNUSED]`/`[USED]` tag appeared anywhere in this session's output** — confirms the deprecation actually held in practice, not just in the reference file's own text.

**Re-audit (later, triggered when Mode A's rules have moved since this file was last touched):**
- Has a new page type been added to Mode A's lineup (a new conditional page, a new Guarantee) that Phase 1's crawl prioritization and Phase 7's signal checks don't yet name? A page type that exists in `page-mapping.md` but not here will get silently bucketed into "other" — the exact problem this redesign fixed once already.
- Has the KD ceiling, secondary floor, or any other numeric threshold changed in the keyword-research rules since this file's checks were written? Confirm every hardcoded number here (KD ≤28, 5+/3+ secondaries, 20%+ decay, position 5–15) still matches the current rule, not a stale copy of an earlier version.
- Has `output-formats.md` § MODE B Audit Output Format changed shape without this file's pointer being re-verified against it? The two must stay in sync by one of them deferring to the other, never by both independently assuming they still agree.

**Any item above that fails sends *this specific audit session's output* back for correction before delivery** — not a note added alongside a flawed delivery. A genuine excuse for one of these failing is rare (most of these are binary — a check either ran correctly or didn't) and should be treated with real suspicion before being accepted rather than fixed.
