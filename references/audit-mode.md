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
| 🔵 UNUSED | Info | Blog cluster in keyword-cluster.txt marked [UNUSED] — post not yet built | Schedule for next content sprint |
| ✅ PASS | Good | Primary keyword correctly implemented in all required positions | No action needed |
| 💡 BONUS | Opportunity | New keyword signal spotted on site not in original plan — potential cluster to add | Add to keyword-map.md and keyword-cluster.txt |
| 📉 DECAY | High | Page's clicks/impressions dropped materially vs the previous period, per GSC's Compare mode (live) or a trend column (fallback export) | Route to Refresh Queue — content update, not a new page |
| 🎯 STRIKING DISTANCE | Opportunity | Query already getting impressions at position 5–15 but isn't a planned secondary | Add as secondary or strengthen on-page signal — this is the cheapest ranking gain available |
| 🔀 MISMATCH | High | Page is planned for keyword A but GSC data (live read or fallback export) shows it actually earning impressions for keyword B | Reassess: retarget the page to B, or reinforce A's on-page signal if B is a false read |

---

## AUDIT PHASE 1 — Site Crawl & Keyword Extraction

### Crawl Protocol

1. **Fetch homepage** via web_fetch — extract: title tag, meta description, H1, first 200 words of body copy, FAQ questions, schema types present, navigation links
2. **Extract all internal links** from homepage navigation and footer — build page inventory
3. **Fetch each inner page** — extract same fields: title, meta, H1, first 200 words, any FAQ content, schema type
4. **Prioritise crawl order:** homepage → category pages → product pages → blog posts → FAQ page → other
5. **Cap at 40 pages** per audit session. For larger sites, crawl the most important pages first (homepage, top categories, top products by URL position depth), note how many were skipped.

### What to Extract Per Page

For every page crawled, record:

```
URL: [full URL]
Page Type: Homepage / Category / Product / Blog / FAQ / Other
Title Tag: [extracted — note if truncated >60 chars]
Meta Description: [extracted — note if outside 130–155 chars]
H1: [extracted — note if missing or multiple H1s found]
First 100 Words: [extracted]
Keywords Detected: [list of keyword signals visible in title+H1+meta+body]
Schema Types Found: [Article / Product / FAQPage / Organization / etc]
FAQ Questions Found: [list if any]
Internal Links Out: [count + sample destinations]
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
| Primary keyword in title tag | Exact match or close variant in first 4 words | 🔴 CRITICAL if missing |
| Primary keyword in H1 | Exact match or close variant | 🔴 CRITICAL if missing |
| Primary keyword in meta description | Present anywhere in meta | 🟠 WARNING if missing |
| Primary keyword in first 100 words | Present at least once | 🟠 WARNING if missing |
| Secondary keywords present | At least 3 of the planned secondaries (5–8) appear somewhere on page | 🟡 DRIFTED if fewer than 3 |
| Planned secondary count meets the floor | keyword-map.md shows 5+ secondaries planned for this page (homepage: 3+) | 🟠 WARNING if the *plan itself* is under floor — this page was mapped before the 5+ rule and needs re-running through Phase 4/5 supplementation, not just a content fix |
| Title tag length | 60 chars or under | 🟡 DRIFTED if over |
| Meta description length | 130–155 chars | 🟡 DRIFTED if outside band |
| One H1 only | Exactly one H1 tag | 🟠 WARNING if multiple |
| Definition hook present | A 1–2 sentence direct answer in first 150 words | 🟡 DRIFTED if missing |

### If no keyword-map.md is available

Skip the comparison step. Work entirely from the Detected Keyword Map built in Phase 1. Flag pages where:
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

| Type | Description | Action |
|------|-------------|--------|
| True orphan | Page exists, no internal links pointing to it, no keyword assignment | 🟣 ORPHAN — assign keyword or delete |
| Unassigned page | Page has internal links but no keyword assignment in the plan | 🟣 ORPHAN — assign a keyword cluster |
| Thin page | Page exists and is linked but has under 300 words and no clear keyword | 🟣 ORPHAN — expand with keyword content or consolidate |
| Legacy page | Page appears to be old/outdated content with no current keyword relevance | 🟣 ORPHAN — redirect to relevant current page or noindex |

**Output per orphan:**
```
🟣 ORPHAN: [URL]
  Discovered via: [how found — nav link / internal link / sitemap]
  Content summary: [1 sentence on what the page contains]
  Recommendation: Assign keyword cluster "[cluster]" / Consolidate into [URL] / Delete + redirect to [URL]
```

---

## AUDIT PHASE 5 — Blog Cluster Status Check

### If keyword-cluster.txt is available

Read the [UNUSED] / [USED] status of every cluster. For each [UNUSED] cluster, check whether a blog post for that topic now exists on the live site (the build may have happened but the file wasn't updated).

**Match logic:** a cluster is considered BUILT if a crawled blog URL contains the primary keyword in its slug, title, or H1.

Update status accordingly:
- Found on site → change [UNUSED] to [USED] in the updated keyword-cluster.txt
- Not found on site → keep [UNUSED], flag in audit summary as pending

### If no keyword-cluster.txt is available

Crawl all blog posts found on the site. For each post, extract:
- Primary keyword (from title/H1)
- Approximate topic cluster
- Whether it has a FAQ section
- Schema type implemented

Build a **Blog Inventory** showing what's live and what gaps remain based on the niche.

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
- Key brand names in the niche with no brand page
- Common buyer questions with no FAQ answer
- Comparison topics (X vs Y) with no blog post

---

## AUDIT PHASE 7 — AI/GEO Signal Check

Run these checks on the crawled pages. Flag missing signals.

| Signal | Check | Severity if Missing |
|--------|-------|-------------------|
| FAQ Schema | FAQPage JSON-LD present on FAQ page and homepage | 🟠 WARNING |
| Speakable Schema | `.brand-statement` or `.faq-answer-speakable` class present on homepage | 🟡 DRIFTED |
| Brand entity statement | Clear 1–2 sentence brand description in first 200 chars of homepage body | 🟠 WARNING |
| Definition hooks | 1–2 sentence direct answer in first 150 words of blog posts | 🟡 DRIFTED |
| Organization schema | Present on homepage with `knowsAbout`, `areaServed`, `sameAs` fields | 🟠 WARNING |
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

Append this section to keyword-map.md under a `## Performance Validation` header, same pattern as the other audit sections. Add any new Striking Distance keywords to the relevant page's secondary list in the main allocation table (respecting the existing 5+ floor and cannibalisation registry — a Striking Distance keyword is still subject to the same "not already used elsewhere" check as any other secondary).

---

## Audit Output — What Gets Updated

### 1. Updated keyword-map.md

Add an **Audit Status** column to the existing allocation table:

```
| Cluster | Primary KW | Vol | KD | Tier | Intent | Assigned URL | Page Type | Status | Audit Status | Audit Notes |
|---------|-----------|-----|-----|------|--------|-------------|----------|--------|-------------|------------|
| [name] | [keyword] | [v] | [k] | T1 | Trans | /url/ | Product | Existing | ✅ PASS | KW in title, H1, meta |
| [name] | [keyword] | [v] | [k] | T1 | Comm | /url/ | Blog | Existing | 🔴 CRITICAL | KW missing from H1 |
| [name] | [keyword] | [v] | [k] | T2 | Info | /url/ | Blog | New | 🔵 UNUSED | Post not yet built |
```

Append new sections at the bottom of keyword-map.md:
- **Cannibalisation Flags** — all ⚫ CANNIBAL findings with merge/differentiate recommendations
- **Orphan Pages** — all 🟣 ORPHAN findings with recommended actions
- **Bonus Opportunities** — all 💡 BONUS findings with proposed clusters
- **Audit Metadata** — date run, pages crawled, overall health score

### 2. Updated keyword-cluster.txt

Update [UNUSED] → [USED] for any clusters confirmed live on the site. Add new clusters from 💡 BONUS findings as [UNUSED] entries at the bottom.

```
# keyword-cluster.txt — updated by audit [date]
# Changes: [n] clusters marked USED, [n] bonus clusters added

[USED]    best electric dirt bikes for kids    /blog/best-electric-dirt-bikes-for-kids/    Commercial    T1    2200w    Article+FAQPage
[UNUSED]  sur-ron light bee x accessories      /blog/sur-ron-light-bee-x-accessories/      Commercial    T2    1400w    Article          ← NEW from audit
```

### 3. In-Chat Audit Summary

Output this in chat immediately after completing all audit phases:

```
## 🔍 Keyword Engine — Audit Complete

**Site:** [domain] ([market])
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
🟣 ORPHAN: [n] pages with no keyword assignment
🔵 UNUSED: [n] blog clusters not yet built
💡 BONUS: [n] new keyword opportunities spotted

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
- docs/keyword-cluster.txt ✅ — [n] clusters marked USED, [n] bonus clusters added

### Recommended Next Actions
1. [Highest priority fix]
2. [Second priority]
3. [Third priority]
4. [Fourth priority]
5. [Fifth priority]
```
