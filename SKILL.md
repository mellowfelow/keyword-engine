---
name: keyword-engine
description: Research skill for ecommerce sites — keyword strategy, niche/taxonomy research, and post-build auditing. Two modes — MODE A (pre-build): paste a keyword list (or just a niche/location to research from scratch) + site URL to produce strategy docs for WebForge; MODE B (post-build audit): site URL only, crawls live site, flags drift/cannibalisation/orphans, updates keyword-map.md and blog-plan.md. Use for: keyword research, niche/shop-taxonomy discovery, clustering, mapping, blog planning, FAQ banks, product gaps, content calendar, SEO/GEO/AEO strategy, AI visibility, keyword audits, cannibalisation checks, or any keyword/research-related task. Do NOT trigger when WebForge is mid-build implementing an existing keyword-map.md.
---

# Keyword Engine

Governed by five core rules (`references/core-rules.md`) that sit above both modes — trusted data sources, the aim is sales, double-check everything, competitor keywords as a standing input, and the Master Audit Gate. Read that file first; it's not optional background, it's what makes every phase below actually airtight rather than just internally consistent.

Two operating modes. Detect which one the user needs at the start of every session and confirm before proceeding.

```
MODE A — STRATEGY (pre-build)          MODE B — AUDIT (post-build)
─────────────────────────────          ──────────────────────────────
Input: keyword paste (or niche/        Input: site URL only
       location to research from
       scratch) + site URL
Runs: before WebForge build            Runs: after WebForge build, manually
Output: 4 strategy docs in docs/       Output: updated keyword-map.md +
       (+ taxonomy-map.md/starter-            blog-plan.md +
       product-list.csv if Phase 0           in-chat audit summary
       ran)
```

**Mode detection:** If the user pastes a keyword list → MODE A, starting at Phase 1. If the user gives only a niche/keyword/location with no list and no existing product list → MODE A, starting at Phase 0 (`references/niche-taxonomy.md`). If the user provides only a URL and asks to check/audit/verify → MODE B. If unclear, ask: "Are you starting a new keyword strategy (Mode A) or auditing a site that's already been built (Mode B)?"

---

## MODE A — Strategy Pipeline

**Runs before WebForge.** Produces the four strategy documents WebForge consumes to build pages, blog posts, and FAQ sections with maximum on-page SEO from day one.

```
INPUTS: raw keyword paste + site URL  — OR — niche/location only (no list, no product list)
    ↓
PHASE 0 → Niche & Taxonomy Discovery   (only when no keyword/product list was given)
    ↓
PHASE 1 → Filter & Clean
PHASE 2 → Intent Classification
PHASE 3 → KD/Volume Scoring & Triage
PHASE 4 → Cluster & De-duplicate        (seeds from Phase 0's taxonomy when it ran)
PHASE 5 → Site Scan & Page Mapping
PHASE 6 → Blog Post Planning
PHASE 7 → FAQ Bank Generation
PHASE 8 → Product Gap Analysis
PHASE 9 → AI/GEO/AEO Visibility Layer
    ↓
OUTPUTS: 4 documents + in-chat summary (+ taxonomy-map.md/starter-product-list.csv if Phase 0 ran)
```

Reference files for MODE A:
- Core rules (governs everything below) → `references/core-rules.md`
- Phase 0 (conditional) → `references/niche-taxonomy.md`
- Phases 1–4 → `references/filter-and-cluster.md`
- Phase 5 → `references/page-mapping.md`
- Phases 6–7 → `references/content-planning.md`
- Phase 8 → `references/product-gaps.md`
- Phase 9 → `references/ai-visibility.md`
- Output formats → `references/output-formats.md`
- Semrush/platform-link operational workflow (how every phase above actually sources real data, per Rules 1 and 4) → `references/semrush-workflow.md`

---

## MODE B — Audit Pipeline

**Runs after a WebForge build, triggered manually.** Crawls the live site, reverse-engineers the current keyword state from what's actually on the pages, compares against the plan, and updates the strategy docs to reflect reality.

```
INPUT: site URL only
    ↓
AUDIT PHASE 1 → Site Crawl & Keyword Extraction
AUDIT PHASE 2 → Implementation Check (vs keyword-map.md plan)
AUDIT PHASE 3 → Cannibalisation Scan
AUDIT PHASE 4 → Orphan Page Detection
AUDIT PHASE 5 → Blog Post Status Check
AUDIT PHASE 6 → Strategy Gap Analysis (new opportunities)
AUDIT PHASE 7 → AI/GEO Signal Check
AUDIT PHASE 8 → Performance Validation (live GSC via in-app browser, falls back to export)
    ↓
OUTPUTS: updated keyword-map.md + blog-plan.md + in-chat audit summary
```

→ Read `references/audit-mode.md` for full audit phase instructions, including Phase 8 (Performance Validation — reads live GSC data via the in-app browser's logged-in session by default).
→ Read `references/output-formats.md` § MODE B Audit Output Format for update templates.

---

## Session Startup Protocol

**Step 1 — Detect mode** (see Mode Detection above). Confirm with the user before proceeding.

**MODE A startup — ask for these if not provided:**
- SITE URL, SITE MARKET, NICHE SUMMARY, EXISTING PAGE LIST (optional — skill crawls if not pasted)
- **Either** KEYWORD PASTE (Keyword / Volume / KD / CPC / Intent columns) or an existing product list — proceed straight to Phase 1. **Or**, if neither exists and the user only gave a niche/keyword to build a shop from scratch, a TARGET MARKET/LOCATION — run Phase 0 first (`references/niche-taxonomy.md`), which produces the taxonomy/stock list AND, immediately after, the keyword paste Phase 1 actually runs on (generated from that taxonomy's own terms via the Semrush link — see `niche-taxonomy.md` § Generating the keyword paste Phase 1 needs).
- COMPETITOR SEMRUSH EXPORT (optional): a competitor's Organic Research or Keyword Gap export does double duty — it unlocks Competitor Gap Analysis (Phase 8) AND becomes a real-data source for secondary keyword supplementation (Phase 4, ranked above Google related searches since it carries actual Vol/KD/CPC). No API access used or assumed — this is a manual export, same as the site's own keyword data. Skip cleanly if not provided.
- SITE-SEARCH QUERY EXPORT (optional): a Query/Count export from the site's own internal search (Shopify, WooCommerce, etc. all support this) becomes the top-priority source for secondary keyword supplementation (Phase 4) — real first-party intent beats generic related-search data. Skip cleanly if not provided.

**MODE B startup — URL only:**
- SITE URL is all that's needed. Skill crawls the live site, extracts what's there, and builds its own current keyword picture from scratch. No docs or keyword paste required.
- **EXISTING DOCS (optional):** if `keyword-map.md`, `blog-plan.md`, and/or `taxonomy-map.md` are pasted or already in context, the audit compares against them directly instead of working purely from the reverse-engineered crawl — richer findings (planned-vs-live drift, Guarantee Flag checks against the actual taxonomy rather than an assumed one, launch-batch-floor coverage) become possible. Skip cleanly if not provided; the audit still runs from the crawl alone.
- **SEMRUSH/PLATFORM LINK (optional):** if a refreshed link is provided this session, the audit can re-check a live primary keyword's KD against the ≤28 ceiling and catch difficulty drift (refresh-before-read discipline applies here too — see `references/semrush-workflow.md`). Without it, skip that specific check — never assume or estimate KD without the actual data, same discipline Phase 1 applies to every other filter in this skill: real data or skip, never a guess.
- **GSC PERFORMANCE DATA (Audit Phase 8):** the skill reads this live, via the in-app browser's already-logged-in Search Console session — no paste needed, no API used. Navigate to `search.google.com/search-console`, match the property by domain, and pull the Performance report (Queries + Pages, Compare-to-previous-period on) directly. Only fall back to asking for a manual CSV export if the property isn't accessible in the logged-in account or the browser session isn't available. If neither works, skip Phase 8 cleanly and say so — never block the rest of the audit on it.

**One site = one session.** Never mix keyword sets across different site domains.

---

## Phase 0 — Niche & Taxonomy Discovery (conditional)

→ Read `references/niche-taxonomy.md`

**Only runs when the user supplied a niche/keyword instead of a ready keyword list or existing product list.** Produces a full, stockable shop taxonomy from scratch (`taxonomy-map.md` + `starter-product-list.csv`), gated by a hard viability check (is this a real, sellable, non-dead product category in the stated market?) and a legal/compliance flag where relevant. **Phase 0 doesn't produce the keyword paste Phase 1 needs** — it answers "what to sell," not "which keywords to target." Immediately after Step H, use the Semrush/platform link to generate that keyword export from the taxonomy's own terms before handing off to Phase 1 — see `niche-taxonomy.md` § Generating the keyword paste Phase 1 needs. Every category/subcategory Phase 0 produces also becomes a seed cluster that Phase 4 clusters against — see `niche-taxonomy.md` § Feeding into clustering. Skip this phase entirely and go straight to Phase 1 whenever a keyword list or product list already exists.

---

## Phase 1 — Filter & Clean

→ Read `references/filter-and-cluster.md` § Filtering Rules

Run these checks in order on the raw paste:

1. **Niche relevance check** — drop any keyword with zero semantic connection to the site's niche
2. **Volume floor** — **intent-sensitive, not flat**: Transactional/Question 20+, Commercial/Informational 50+, Navigational no floor (see `references/filter-and-cluster.md` for why a flat floor throws away real money)
3. **KD ceiling** — tightened: primaries are hard-capped at KD ≤28 (nothing above 28 is ever a primary, no exceptions). Secondaries/LSI default to the same ≤28, extending into a 29–35 fallback band only when genuinely needed to hit the secondary minimum. **Nothing above KD 35 is used anywhere, under any exception** — no Supporting Pool, no revisit-later appendix. Drop it, full stop, regardless of volume.
4. **Deduplication** — remove exact duplicates; merge near-duplicates (singular/plural, spelling variants) keeping the higher-volume form
5. **Brand contamination check** — flag competitor brand names; move to a separate "Competitor Brands" list for comparison content only, never product pages
6. **Geography tag** — flag US vs UK spelling/intent variants (e.g. "dirt bike" vs "off-road motorbike") — apply site market filter, drop the wrong market's variants
7. **Cannibalisation pre-check** — flag any two keywords that would logically target the same page URL

Output after Phase 1:
- ✅ Primary Pool (KD ≤28, volume per the intent-sensitive floor above)
- 🟡 Secondary Fallback Pool (KD 29–35 — secondary/LSI use only, and only when needed to hit the secondary minimum; never a primary)
- 🔴 Dropped List (below the applicable floor, or KD above 35 — no exception) — show count only
- 🏷️ Competitor Brand List — held for comparison content

---

## Phase 2 — Intent Classification

→ Read `references/filter-and-cluster.md` § Intent Rules

Classify every keyword in the Primary Pool and the Secondary Fallback Pool:

| Intent | Signals | Maps To |
|--------|---------|---------|
| **Transactional** | buy, price, for sale, cheap, deal, order, shop, discount, near me, shipping | Product pages, category pages |
| **Commercial** | best, top, review, vs, recommended, compare, worth it, pros cons | Blog posts (comparison/review), category pages |
| **Informational** | how, what, why, guide, tips, explained, tutorial, learn | Blog posts (guides), pillar pages |
| **Question** | does, can I, is it, how long, will, should, do I need | FAQ bank entries — homepage, FAQ page, AND a page-specific mini-FAQ on any mapped page with question-intent keywords in its cluster (Phase 7) |
| **Navigational** | brand name + model | Individual Brand pages (anchored on Navigational primaries by default — not to be confused with the separate aggregator "Brand Hub" page, Phase 5), individual product pages |

**Priority order for page assignment:** Transactional → Commercial → Informational → Question → Navigational. When a keyword matches more than one category's signals (e.g. "how much does it cost" = Transactional + Question), the higher-priority category always wins — never split the difference. Worked examples in `references/filter-and-cluster.md`.

**Blog anchoring — reversed, confirmed override of the old Transactional-on-blog ban.** A missing page has three causes, not two: a true orphan Transactional keyword (vol 20–99, never clustered) is blog-eligible (Reason A); a true orphan Informational keyword (never clustered, vol <200) is also blog-eligible, as last-resort filler only (Reason A2); real volume with no matching product/category routes to a Gap Flag instead, never to blog, regardless of volume (Reason B). Sourcing order is strict across all blog-eligible clusters: **Transactional (Reason A) → Commercial → Informational (including Reason A2)**, with Informational never the backbone. Full carve-out and routing detail in `references/page-mapping.md` §7.

**Local intent (situational — only sites with a physical location/service area):** "near me" and city/region-modified queries route to a dedicated location page, never bolted onto the general category page as a secondary. Skip entirely for a ship-anywhere ecommerce site. Full rules in `references/filter-and-cluster.md` § Local Intent Layer.

---

## Phase 3 — KD/Volume Scoring & Triage

→ Read `references/filter-and-cluster.md` § Scoring Rules

Score every keyword in the Primary Pool with a Priority Tier (KD bands calibrated to SEMrush KD%, tightened for realistic performance on a smaller/newer site — see `references/filter-and-cluster.md`):

| Tier | KD | Time to Rank | Action |
|------|-----|-------------|--------|
| 🥇 **T1 — Quick Win** | 0–19 | 1–3 months | Build dedicated pages first |
| 🥈 **T2 — Worth Targeting** | 20–28 | 2–4 months | Build pages, good content required |
| 🟡 **Secondary Fallback (no Tier label)** | 29–35 | N/A — never a primary | Secondary/LSI only, used only when needed to hit the secondary minimum |

Tier (T1/T2) applies to the **primary keyword only** — nothing above KD 28 is ever a primary. A secondary pulled from the 29–35 fallback band carries no Tier label of its own.

(Volume floor is the intent-sensitive one from Phase 1 — 20+ for Transactional/Question, 50+ for Commercial/Informational.)

**Never build a new page for a keyword above KD 28.** Keywords in the 29–35 fallback band are secondary/LSI use only, on pages that already exist for a qualifying T1/T2 primary — never a dedicated page of their own, and never used at all above KD 35.

**Opportunity Score** — within a tier, or when picking which keyword becomes a cluster's primary, rank by `((Volume × Intent Weight) / 10) − (KD × 2) + (CPC × 3)`, not volume/KD alone. This folds CPC in as a commercial-value signal so genuinely valuable keywords win, not just easy ones. Full formula and intent weights in `references/filter-and-cluster.md`.

**Primary selection is gated by intent before scoring runs.** Transactional candidates are scored first; only if zero qualify does the pool open to Commercial. Secondaries run the inverse order (Commercial first, Transactional second). This is a hard gate on top of Opportunity Score, not replaced by it — full rule, carve-outs (Individual Brand pages, homepage/shop), in `references/filter-and-cluster.md` § Primary/Secondary Intent Priority.

**No high-volume outlier exception — removed.** A keyword above KD 35 is dropped regardless of volume, even at Vol 2000+. There is no "Revisit in 6 months" section — chasing a keyword that takes real authority to rank for isn't worth it even when tempting, high-volume data is attached.

**Low-KD Rescue (the mirror case):** a Transactional/Commercial keyword below the volume floor but **KD ≤ 15** isn't dropped — it's an easy, real, scored win. Route it to the Secondary Pool (never a dedicated page) and prioritize it first when supplementing a thin cluster's secondaries in Phase 4. **KD ≤ 10** is the strongest rescue tier — flag distinctly. See `references/filter-and-cluster.md`.

**Not every passing keyword is worth building for.** Before locking in T1/T2 keywords for a dedicated page, spot-check against situational red flags — marketplace-dominated SERPs (Amazon/eBay/Walmart a small site can't realistically outrank), non-commercial SERPs for a nominally "commercial" keyword, or a structurally irrelevant audience. This is a judgment layer on top of the numeric bands, not a replacement for them — flag the call in the map's notes rather than silently dropping or silently keeping. Full detail in `references/filter-and-cluster.md` § Situational Drop.

---

## Phase 4 — Cluster & De-duplicate

→ Read `references/filter-and-cluster.md` § Clustering Rules

**If Phase 0 ran:** every category/subcategory in `taxonomy-map.md` is a seed cluster — check each natural cluster against the seeds first; a topical match extends the seed rather than forming an independent cluster. See `references/filter-and-cluster.md` § Seed Clusters.

Group keywords into clusters. Each cluster = one URL.

**Clustering criteria (in order):**
1. Same search intent
2. Would the same page satisfy all these queries?
3. Semantic overlap — same topic, different phrasing
4. Modifier patterns — `best [X]`, `[X] for sale`, `[X] review` cluster together when X is the same product type

**Cluster size rules:**
- Minimum 2 keywords per cluster at the raw-clustering stage (orphan singles → held for review)
- Maximum 15 keywords per cluster (split if larger)
- Each cluster gets exactly 1 primary keyword (highest **Opportunity Score** — not raw Vol/KD alone, see Phase 3)
- **⭐ Minimum 5, maximum 8 secondary keywords per cluster — this is a floor, not a target.** Every page-mapped cluster must reach 1 primary + 5+ secondary before the map is finalized (homepage AND the top-level shop page are the two lighter exceptions, treated identically — see Phase 5).
- **Supplementation when a cluster is thin:** if a site-search export was provided, mine it first (real first-party query data beats everything else). Then broaden within the existing Vol/KD pools, then mine a competitor SEMrush export if one was provided (real Vol/KD/CPC data from the competitor's ranking keywords, scored normally like the site's own data), then pull Google related searches (`web_fetch` the live SERP), then generate transactional modifiers (`buy [X]`, `[X] for sale`, `cheap [X]`, `[X] price`, `[X] near me`, etc.) matched to the cluster's actual intent. Site-search, related-search, and generated keywords have no real Vol/KD/CPC and **inherit the cluster's Tier** as a labeling convenience; pool-broadening and competitor-sourced keywords carry real KD data and follow Phase 3's actual Tier rule from that KD (no Tier label at all if it lands in the 29–35 fallback band — real data doesn't earn an exception). All get labelled `[site-search]`, `[competitor]`, `[related-search]`, or `[generated]` in the output so the source stays transparent. Never pad with off-topic keywords just to hit the count — ship an honest "3/5, niche too narrow" instead. Full detail in `references/filter-and-cluster.md`.
- Remaining cluster keywords = LSI/supporting role

**Cannibalisation enforcement — three levels, not just URLs:**
- One cluster = one URL. Hard rule.
- If two clusters would logically land on the same URL, merge them
- Never assign the same keyword to two clusters — **this includes secondaries and supplemented keywords, not just primaries.** Supplementation pulls from shared pools (Low-KD Rescue, generated modifiers, related searches) across many clusters, so secondary-level collisions are a real risk now — keep a running used-keyword registry as you go, not a check only at the end.
- Same principle for FAQ questions: one buyer question gets answered on exactly one page (homepage FAQ, the FAQ page, or a page-level mini-FAQ) — never duplicated across two. Full three-level audit in `references/page-mapping.md` § Cannibalisation Audit.

---

## Phase 5 — Site Scan & Page Mapping

→ Read `references/page-mapping.md`

**If site URL provided:** Use web_fetch to crawl the homepage and key pages. Extract: page titles, H1s, meta descriptions, existing URL structure, product/category names.

**If page list pasted:** Use that directly.

Map each cluster to a page using this priority (full detail, including page types not condensed here, in `references/page-mapping.md`):

```
1. Existing product page → assign if product match is strong
2. Existing category/brand page → assign if cluster is category-level (individual brand pages anchor on Navigational)
3. Homepage AND top-level shop page → 1 primary + 3-5 secondary only, both equally (lighter than every other page — see references/page-mapping.md for why)
4. Existing blog post → assign to improve it, if informational/commercial and a directly relevant post exists
5. New product page needed → flag as gap
6. New category page needed → flag as gap (cascades into starter-product research once approved)
7. New blog post needed → flag for Phase 6, under the Reason A/B split (see Phase 2 — only true orphans route to blog; real-volume gaps always flag instead)
8. Programmatic pattern set → for catalogs with genuine combinatorial structure (Brand × Category, Size × Type, etc.) at real scale — flag as a page-template set, not individual gaps (see references/page-mapping.md § Programmatic Pattern Pages)
9. Other guaranteed/conditional page types not listed above — FAQ page (guaranteed default), Sale/Deals, Best Sellers/New Arrivals, Compare, Wholesale (all conditional), Brand Hub (3+ brands), utility pages — see references/page-mapping.md § Other Guaranteed/Conditional Page Types for placement rules
```

**Before finalizing any assignment (except homepage and the shop page): run the Secondary Keyword Supplementation check.** If the cluster has fewer than 5 secondary keywords, supplement per Phase 4 before writing the page's entry.

**Mapping output per cluster:**
- Assigned URL (existing or proposed)
- Page type (product / category / individual brand / Brand Hub / homepage / shop / blog / Sale / Best Sellers / New Arrivals / Compare / Wholesale / FAQ / utility / new)
- Primary keyword (highest Opportunity Score)
- Secondary keywords — **5+ minimum (homepage and shop page: 3-5)**, each tagged with its source if supplemented (`[site-search]` / `[competitor]` / `[related-search]` / `[generated]`)
- LSI/supporting keywords (secondary/LSI pool, including any pulled from the 29–35 fallback band)
- On-page requirements: title tag formula, H1 formula, meta description formula, image alt text note
- Journey stage (Awareness/Consideration/Purchase/Loyalty) + the forward/back internal links to its journey-adjacent content — see `references/page-mapping.md` § Journey-Stage Internal Linking
- Page-level FAQ (2–4 Q&As) if the cluster has question-intent keywords to draw on — see `references/content-planning.md` § Page-Level FAQ

---

## Phase 6 — Blog Post Planning

→ Read `references/content-planning.md` § Blog Planning

All clusters mapped to "new blog post" get a full brief, under the Reason A/B split (page-mapping.md) that governs which clusters are even blog-eligible — Reason-A Transactional orphans (vol 20–99) and Commercial clusters, never Reason-B (those route to a Gap Flag instead). Maximise the number of posts within that — every viable Reason-A/Commercial cluster gets one, with Informational sourced last as filler.

**Launch batch floor, tiered by niche breadth — not a flat 20.** Every session must deliver a complete launch batch, ready to build immediately, sized per the niche tier (25–30 Micro/Small, up to 100+ Massive — see `references/content-planning.md` § Launch Batch Floor for the full sizing table), toward a 1000+ overall target where the niche supports it. If the natural cluster set falls short of the tier's target, expand it before delivery, real data first and Transactional/Commercial before Informational: broaden Reason-A/Commercial coverage, mine a site-search export for topic angles if one was provided, mine a competitor export for content gaps if one was provided, then mine the site's own catalog for comparison/accessory/buying-guide angles, and finally pull topic ideas from Google related-search mining. Never pad the count with thin, near-duplicate topics just to hit the target — if genuine expansion can't reach it, say so explicitly and show the real number with the reasoning, rather than silently under-delivering or manufacturing filler. See `references/content-planning.md` § Launch Batch Floor for the full floor + expansion strategy.

**Blog post brief includes:**
- Post title (H1) — keyword-first, click-worthy
- Meta description (150–160 chars, includes primary keyword)
- Target primary keyword + secondary keywords
- Word count recommendation, by cluster size (see `references/content-planning.md` § Word Count by Cluster Size for the authoritative table): 2–4 kw → 800–1200w; 5–8 kw → 1200–2000w; 9–12 kw → 2000–3000w; 13+ kw → 3000–5000w pillar
- Content type: guide / comparison / listicle / review / explainer / roundup / care & maintenance guide
- Proposed URL slug
- H2/H3 outline (full section structure)
- Internal links: which existing pages to link to + which pages should link to this post
- CTA recommendation (what should the reader do next — buy, browse category, contact)
- Suggested images: number, type (product shot / lifestyle / diagram / infographic), alt text formulas
- Schema type: Article / HowTo / FAQPage / Review
- FAQ section: 3–5 questions derived from question-intent keywords in the cluster
- Funnel position: Top / Middle / Bottom / Loyalty (post-purchase — a fourth, additive category, sourced last once Top/Middle/Bottom are satisfied, not a separate quota)

**Pillar + Cluster architecture:** Identify the top 3–5 highest-volume informational topics. These become pillar posts (3000w+). All related cluster posts link back to the relevant pillar.

**Content calendar:** Sequence blog posts by Tier (T1 first), then by funnel position (Bottom → Middle → Top), with Loyalty content filled in last once Bottom/Middle/Top are satisfied — into the backlog, not a dedicated week block. Output a 12-week publishing schedule.

---

## Phase 7 — FAQ Bank Generation

→ Read `references/content-planning.md` § FAQ Rules

All question-intent keywords + question signals from across all clusters feed into the FAQ bank.

**FAQ Homepage (6–8 questions):**
- Highest-impact questions only
- Prioritise questions about buying, pricing, shipping, product types
- Each answer: 40–55 words, conversational, includes primary keyword naturally
- Includes JSON-LD FAQPage schema block

**FAQ Page (full bank, grouped by theme):**
- All question keywords organised into thematic sections
- Each answer: 50–65 words, includes 1–2 supporting keywords naturally
- Speakable schema flagged on top answers
- Each answer optimised for featured snippet extraction

**⭐ Page-Level FAQ (every mapped page, not just homepage + FAQ page):** a 2–4 question mini-FAQ on every product/category/individual-brand/Brand-Hub/shop/blog/active-Sale/Best-Sellers/New-Arrivals/Compare/Wholesale page that has question-intent keywords in its cluster (or an obvious buyer question even without one — use judgment, don't invent filler). This is the biggest lever for organic keyword coverage in this phase — each page-level FAQ answer is unique indexable content that lets one page compete for query variations it otherwise can't touch, without diluting the page's primary-keyword focus. Skip only when a cluster genuinely has nothing to draw on. Its own FAQPage schema instance per page. Full rules in `references/content-planning.md` § Page-Level FAQ.

**FAQ rules:**
- Never answer a question with "it depends" — always give a concrete answer
- Every answer must include a soft CTA or internal link
- Questions about competitor products → handled diplomatically, steer to your products

---

## Phase 8 — Product Gap Analysis

→ Read `references/product-gaps.md`

Scan all clusters. Flag any transactional or commercial cluster where no existing page can absorb it.

**Full proposal per gap:**
- Product type (what it is)
- Suggested category it belongs to
- Suggested brands to stock (inferred from keyword data — if "Sur-Ron electric dirt bike" appears as a keyword cluster with no Sur-Ron page, that's a brand gap)
- Estimated demand signal (primary keyword volume + all cluster keyword volumes combined)
- Suggested URL (e.g. `/brands/sur-ron/` or `/electric-dirt-bikes/youth/`)
- Primary keyword to target (highest Opportunity Score)
- **Secondary keywords for that page — fully assembled to the 5+ floor, not just listed.** Run every gap through the same Secondary Keyword Selection Rules + Supplementation used for live pages (`references/filter-and-cluster.md`) before it's written into product-gaps.md. **The point of this: when the client decides to build the gap, the keyword package is already complete — no extra research pass, no gap between the decision and the build.**
- **Recommended Price** — a single number, not a range, sourced from competitor pricing research. Re-check before approval if competitor pricing has moved since this was generated.
- Page-level FAQ candidates, pre-drafted for the same reason (2–4 Q&As where the cluster supports it)
- Priority tier (T1 gaps first)

**Five gap types, kept distinct: Brand, Product, Category, Accessory, Competitor.** Don't collapse Accessory gaps (accessory/part patterns with no matching page) into generic Product gaps — `product-gaps.md`'s own output tracks all five separately.

**Competitor Gap (optional — requires a competitor SEMrush export):** if the user provides a competitor's SEMrush Organic Research/Keyword Gap export, cross-reference it against this site's Primary Pool and page inventory to find keywords the competitor visibly ranks for that this site has no coverage for at all. No API access — export only, same as the site's own keyword data. Skip cleanly if not provided. Full workflow in `references/product-gaps.md` § Competitor Gap Analysis.

**Link Magnet Candidates:** once per session, after all gaps are flagged, scan for 1–2 realistic link-worthy content candidates (free tool, original data, resource hub, comparison, downloadable, embeddable widget, digital PR hook) — the on-page lever for earning backlinks and referral traffic, not just search rankings. Quality over volume — state plainly if no strong candidate exists rather than padding the list. Full detail in `references/product-gaps.md` § Link Magnet Candidates.

---

## Phase 9 — AI/GEO/AEO Visibility Layer

→ Read `references/ai-visibility.md`

Run this layer across all outputs — it annotates the keyword map and content plan with AI visibility signals.

**Seven signals applied to every page and blog post:**

1. **FAQ Schema** — every page with 2+ question-intent keywords in its cluster gets a FAQPage JSON-LD block planned
2. **Speakable Schema** — flag the single best FAQ answer on each page for `speakable` schema (voice + AI assistant readability)
3. **Entity Coverage** — check: does each page clearly name the product entity, brand entity, and (where relevant) location entity? Flag gaps. The homepage's and shop page's own primary+secondary keywords are the designated source for the Organization schema's `knowsAbout[]` array — no separate tracking, just a read off what Phase 5 already assigned to those two pages.
4. **Featured Snippet Hooks** — every informational/question keyword cluster gets a "definition hook": a 1–2 sentence plain-language answer in the first 150 words of the page
5. **llms.txt Priority Map** — at the end of the session, output a prioritised list of URLs to include in `llms.txt`, ranked by topical authority and AI answer relevance
6. **SERP Feature Targeting** — check the live SERP for the primary keyword (snippet/PAA/image pack/shopping pack) and structure the page to match what's actually showing, instead of one generic format for every page
7. **AI Overview / AI Assistant Citation Optimization** — format the Definition Hook (Signal 4) for AI-citation extraction specifically: fact-first, one claim per sentence, number anchored early, plain-text extractable

**Local Business Schema (situational):** sites with a physical location/service area get `LocalBusiness` schema (address, geo, openingHours, areaServed) on each location page instead of the generic Organization schema — one block per location, never shared. Skip for ship-anywhere ecommerce sites. See `references/ai-visibility.md` § Local Business Schema.

---

## Output Documents

Produce all four documents at the end of every session (plus two more if Phase 0 ran).
→ See `references/output-formats.md` for exact templates.

| Document | WebForge Uses It For | Contents |
|----------|---------------------|---------|
| `keyword-map.md` | Page meta, H1s, on-page copy | Full keyword allocation table — every keyword assigned to a URL with tier, intent, role |
| `blog-plan.md` | Blog post builds — titles, outlines, schema, internal links; also the blog build queue | Full brief for every planned blog post + 12-week content calendar. Each post carries a `Pending`/`Built` Status field — this is the blog post build queue now; there is no separate `keyword-cluster.txt` file. |
| `faq-bank.md` | Homepage FAQ section + FAQ page build + FAQPage schema | All FAQ Q&As with JSON-LD schema blocks, grouped by theme |
| `product-gaps.md` | Product/category page creation decisions | All product/category/brand gap proposals with full demand analysis |
| `taxonomy-map.md` (only if Phase 0 ran) | Shop structure, category pages to build | Full category→subcategory tree, top brands/products with confidence tags, sources, viability verdict |
| `starter-product-list.csv` (only if Phase 0 ran) | Initial stock list | Flat category/subcategory/product/brand/confidence list — hand straight to a supplier |

**⚠️ WebForge Rule 12 — all strategy documents go in `docs/` only.**
Never place them in `public/` or include them in any deploy ZIP. These are internal strategy files — putting them on the live site hands competitors the entire plan. WebForge enforces this at crosscheck.

**In-chat summary after each session:**
- Total keywords processed
- Keywords kept vs dropped
- Pages mapped
- Blog posts planned
- FAQ entries generated
- Product gaps found
- AI visibility flags raised
