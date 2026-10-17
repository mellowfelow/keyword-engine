---
name: keyword-engine
description: Keyword strategy and audit skill for ecommerce sites. Two modes — MODE A (pre-build): paste keywords + site URL to produce strategy docs for WebForge; MODE B (post-build audit): site URL only, crawls live site, flags drift/cannibalisation/orphans, updates keyword-map.md and keyword-cluster.txt. Use for: keyword research, clustering, mapping, blog planning, FAQ banks, product gaps, content calendar, SEO/GEO/AEO strategy, AI visibility, keyword audits, cannibalisation checks, or any keyword-related task. Do NOT trigger when WebForge is mid-build implementing an existing keyword-map.md.
---

# Keyword Engine

Two operating modes. Detect which one the user needs at the start of every session and confirm before proceeding.

```
MODE A — STRATEGY (pre-build)          MODE B — AUDIT (post-build)
─────────────────────────────          ──────────────────────────────
Input: keyword paste + site URL        Input: site URL only
Runs: before WebForge build            Runs: after WebForge build, manually
Output: 5 strategy docs in docs/       Output: updated keyword-map.md +
                                               keyword-cluster.txt +
                                               in-chat audit summary
```

**Mode detection:** If the user pastes a keyword list → MODE A. If the user provides only a URL and asks to check/audit/verify → MODE B. If unclear, ask: "Are you starting a new keyword strategy (Mode A) or auditing a site that's already been built (Mode B)?"

---

## MODE A — Strategy Pipeline

**Runs before WebForge.** Produces the five strategy documents WebForge consumes to build pages, blog posts, and FAQ sections with maximum on-page SEO from day one.

```
INPUTS: raw keyword paste + site URL
    ↓
PHASE 1 → Filter & Clean
PHASE 2 → Intent Classification
PHASE 3 → KD/Volume Scoring & Triage
PHASE 4 → Cluster & De-duplicate
PHASE 5 → Site Scan & Page Mapping
PHASE 6 → Blog Post Planning
PHASE 7 → FAQ Bank Generation
PHASE 8 → Product Gap Analysis
PHASE 9 → AI/GEO/AEO Visibility Layer
    ↓
OUTPUTS: 5 documents + in-chat summary
```

Reference files for MODE A:
- Phases 1–4 → `references/filter-and-cluster.md`
- Phase 5 → `references/page-mapping.md`
- Phases 6–7 → `references/content-planning.md`
- Phase 8 → `references/product-gaps.md`
- Phase 9 → `references/ai-visibility.md`
- Output formats → `references/output-formats.md`

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
AUDIT PHASE 5 → Blog Cluster Status Check
AUDIT PHASE 6 → Strategy Gap Analysis (new opportunities)
AUDIT PHASE 7 → AI/GEO Signal Check
AUDIT PHASE 8 → Performance Validation (live GSC via in-app browser, falls back to export)
    ↓
OUTPUTS: updated keyword-map.md + keyword-cluster.txt + in-chat audit summary
```

→ Read `references/audit-mode.md` for full audit phase instructions, including Phase 8 (Performance Validation — reads live GSC data via the in-app browser's logged-in session by default).
→ Read `references/output-formats.md` § Audit Output for update templates.

---

## Session Startup Protocol

**Step 1 — Detect mode** (see Mode Detection above). Confirm with the user before proceeding.

**MODE A startup — ask for these if not provided:**
- SITE URL, SITE MARKET, NICHE SUMMARY, KEYWORD PASTE (Keyword / Volume / KD / CPC / Intent columns), EXISTING PAGE LIST (optional — skill crawls if not pasted)
- COMPETITOR SEMRUSH EXPORT (optional): a competitor's Organic Research or Keyword Gap export does double duty — it unlocks Competitor Gap Analysis (Phase 8) AND becomes a real-data source for secondary keyword supplementation (Phase 4, ranked above Google related searches since it carries actual Vol/KD/CPC). No API access used or assumed — this is a manual export, same as the site's own keyword data. Skip cleanly if not provided.
- SITE-SEARCH QUERY EXPORT (optional): a Query/Count export from the site's own internal search (Shopify, WooCommerce, etc. all support this) becomes the top-priority source for secondary keyword supplementation (Phase 4) — real first-party intent beats generic related-search data. Skip cleanly if not provided.

**MODE B startup — URL only:**
- SITE URL is all that's needed. Skill crawls the live site, extracts what's there, and builds its own current keyword picture from scratch. No docs or keyword paste required.
- **GSC PERFORMANCE DATA (Audit Phase 8):** the skill reads this live, via the in-app browser's already-logged-in Search Console session — no paste needed, no API used. Navigate to `search.google.com/search-console`, match the property by domain, and pull the Performance report (Queries + Pages, Compare-to-previous-period on) directly. Only fall back to asking for a manual CSV export if the property isn't accessible in the logged-in account or the browser session isn't available. If neither works, skip Phase 8 cleanly and say so — never block the rest of the audit on it.

**One site = one session.** Never mix keyword sets across different site domains.

---

## Phase 1 — Filter & Clean

→ Read `references/filter-and-cluster.md` § Filtering Rules

Run these checks in order on the raw paste:

1. **Niche relevance check** — drop any keyword with zero semantic connection to the site's niche
2. **Volume floor** — **intent-sensitive, not flat**: Transactional/Question 20+, Commercial/Informational 50+, Navigational no floor (see `references/filter-and-cluster.md` for why a flat floor throws away real money)
3. **KD ceiling** — calibrated to SEMrush KD%: drop anything KD 55+ entirely; move KD 35–54 to "Supporting Pool" (not droppable but not primary) — tightened from the original release since SEMrush KD% under-represents true difficulty for smaller sites
4. **Deduplication** — remove exact duplicates; merge near-duplicates (singular/plural, spelling variants) keeping the higher-volume form
5. **Brand contamination check** — flag competitor brand names; move to a separate "Competitor Brands" list for comparison content only, never product pages
6. **Geography tag** — flag US vs UK spelling/intent variants (e.g. "dirt bike" vs "off-road motorbike") — apply site market filter, drop the wrong market's variants
7. **Cannibalisation pre-check** — flag any two keywords that would logically target the same page URL

Output after Phase 1:
- ✅ Primary Pool (KD 0–34, volume per the intent-sensitive floor above)
- 🟡 Supporting Pool (KD 35–54, same floor)
- 🔴 Dropped List (below the applicable floor or KD 55+) — show count only
- 🏷️ Competitor Brand List — held for comparison content

---

## Phase 2 — Intent Classification

→ Read `references/filter-and-cluster.md` § Intent Rules

Classify every keyword in the Primary and Supporting pools:

| Intent | Signals | Maps To |
|--------|---------|---------|
| **Transactional** | buy, price, for sale, cheap, deal, order, shop, discount, near me, shipping | Product pages, category pages |
| **Commercial** | best, top, review, vs, recommended, compare, worth it, pros cons | Blog posts (comparison/review), category pages |
| **Informational** | how, what, why, guide, tips, explained, tutorial, learn | Blog posts (guides), pillar pages |
| **Question** | does, can I, is it, how long, will, should, do I need | FAQ bank entries — homepage, FAQ page, AND a page-specific mini-FAQ on any mapped page with question-intent keywords in its cluster (Phase 7) |
| **Navigational** | brand name + model | Brand hub pages (anchored on Navigational primaries by default), individual product pages |

**Priority order for page assignment:** Transactional → Commercial → Informational → Question → Navigational. When a keyword matches more than one category's signals (e.g. "how much does it cost" = Transactional + Question), the higher-priority category always wins — never split the difference. Worked examples in `references/filter-and-cluster.md`.

**Blog posts are anchored on Informational primaries by default** (Commercial also routes there for comparison/review posts, but the pillar/guide backbone should be Informational-first — under-serving this misses easy, less-contested ranking opportunities).

**Local intent (situational — only sites with a physical location/service area):** "near me" and city/region-modified queries route to a dedicated location page, never bolted onto the general category page as a secondary. Skip entirely for a ship-anywhere ecommerce site. Full rules in `references/filter-and-cluster.md` § Local Intent Layer.

---

## Phase 3 — KD/Volume Scoring & Triage

→ Read `references/filter-and-cluster.md` § Scoring Rules

Score every keyword in the Primary Pool with a Priority Tier (KD bands calibrated to SEMrush KD%, tightened for realistic performance on a smaller/newer site — see `references/filter-and-cluster.md`):

| Tier | KD | Time to Rank | Action |
|------|-----|-------------|--------|
| 🥇 **T1 — Quick Win** | 0–19 | 1–3 months | Build dedicated pages first |
| 🥈 **T2 — Worth Targeting** | 20–34 | 3–6 months | Build pages, good content required |
| 🟡 **T3 — Supporting** | 35–54 | Never primary | Use as LSI/secondary on existing pages only |

(Volume floor is the intent-sensitive one from Phase 1 — 20+ for Transactional/Question, 50+ for Commercial/Informational.)

**Never build a new page for a T3 keyword.** Use T3 keywords to enrich copy, meta descriptions, image alt text, FAQ answers, and body content on pages that already exist for T1/T2 keywords.

**Opportunity Score** — within a tier, or when picking which keyword becomes a cluster's primary, rank by `((Volume × Intent Weight) / 10) − (KD × 2) + (CPC × 3)`, not volume/KD alone. This folds CPC in as a commercial-value signal so genuinely valuable keywords win, not just easy ones. Full formula and intent weights in `references/filter-and-cluster.md`.

**High-volume outlier rule:** If a keyword is KD 35–54 but Vol 2000+, flag it in a "Revisit in 6 months" section at the end of `keyword-map.md`. Do not assign it now.

**Low-KD Rescue (the mirror case):** a Transactional/Commercial keyword below the volume floor but **KD ≤ 15** isn't dropped — it's an easy, real, scored win. Route it to the Secondary Pool (never a dedicated page) and prioritize it first when supplementing a thin cluster's secondaries in Phase 4. **KD ≤ 10** is the strongest rescue tier — flag distinctly. See `references/filter-and-cluster.md`.

**Not every passing keyword is worth building for.** Before locking in T1/T2 keywords for a dedicated page, spot-check against situational red flags — marketplace-dominated SERPs (Amazon/eBay/Walmart a small site can't realistically outrank), non-commercial SERPs for a nominally "commercial" keyword, or a structurally irrelevant audience. This is a judgment layer on top of the numeric bands, not a replacement for them — flag the call in the map's notes rather than silently dropping or silently keeping. Full detail in `references/filter-and-cluster.md` § Situational Drop.

---

## Phase 4 — Cluster & De-duplicate

→ Read `references/filter-and-cluster.md` § Clustering Rules

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
- **⭐ Minimum 5, maximum 8 secondary keywords per cluster — this is a floor, not a target.** Every page-mapped cluster must reach 1 primary + 5+ secondary before the map is finalized (homepage is the one lighter exception — see Phase 5).
- **Supplementation when a cluster is thin:** if a site-search export was provided, mine it first (real first-party query data beats everything else). Then broaden within the existing Vol/KD pools, then mine a competitor SEMrush export if one was provided (real Vol/KD/CPC data from the competitor's ranking keywords, scored normally like the site's own data), then pull Google related searches (`web_fetch` the live SERP), then generate transactional modifiers (`buy [X]`, `[X] for sale`, `cheap [X]`, `[X] price`, `[X] near me`, etc.) matched to the cluster's actual intent. Site-search, related-search, and generated keywords have no real Vol/KD/CPC and **inherit the cluster's Tier**; pool-broadening and competitor-sourced keywords carry real data and are scored normally. All get labelled `[site-search]`, `[competitor]`, `[related-search]`, or `[generated]` in the output so the source stays transparent. Never pad with off-topic keywords just to hit the count — ship an honest "3/5, niche too narrow" instead. Full detail in `references/filter-and-cluster.md`.
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

Map each cluster to a page using this priority:

```
1. Existing product page → assign if product match is strong
2. Existing category/brand page → assign if cluster is category-level
3. Homepage → 1 primary + 3-5 secondary only (lighter than every other page — see references/page-mapping.md for why)
4. New product page needed → flag as gap
5. New blog post needed → flag for Phase 6
6. New category page needed → flag as gap
7. Programmatic pattern set → for catalogs with genuine combinatorial structure (Brand × Category, Size × Type, etc.) at real scale — flag as a page-template set, not individual gaps (see references/page-mapping.md § Programmatic Pattern Pages)
```

**Before finalizing any assignment (except homepage): run the Secondary Keyword Supplementation check.** If the cluster has fewer than 5 secondary keywords, supplement per Phase 4 before writing the page's entry.

**Mapping output per cluster:**
- Assigned URL (existing or proposed)
- Page type (product / category / brand / homepage / blog / new)
- Primary keyword (highest Opportunity Score)
- Secondary keywords — **5+ minimum (homepage: 3-5)**, each tagged with its source if supplemented (`[site-search]` / `[competitor]` / `[related-search]` / `[generated]`)
- LSI/supporting keywords (T3 pool contributions)
- On-page requirements: title tag formula, H1 formula, meta description formula, image alt text note

---

## Phase 6 — Blog Post Planning

→ Read `references/content-planning.md` § Blog Planning

All clusters mapped to "new blog post" get a full brief. Maximise the number of posts — every viable cluster gets one.

**Minimum 20 fully-briefed posts, day one.** Every keyword-map session must deliver at least 20 complete blog briefs ready to build immediately — not a placeholder list, not "more available on request." If the natural cluster set falls short of 20, expand it before delivery, real data first: broaden the Supporting Pool (KD 35-54) for viable informational/commercial angles, mine a site-search export for topic angles if one was provided, mine a competitor export for content gaps if one was provided, then mine the site's own catalog for comparison/accessory/buying-guide angles, and finally pull topic ideas from Google related-search mining. Never pad the count with thin, near-duplicate topics just to hit the number — if genuine expansion can't reach 20, say so explicitly and show the real number with the reasoning, rather than silently under-delivering or manufacturing filler. See `references/content-planning.md` § Minimum 20 Fully-Briefed Posts for the full floor + expansion strategy.

**Blog post brief includes:**
- Post title (H1) — keyword-first, click-worthy
- Meta description (150–160 chars, includes primary keyword)
- Target primary keyword + secondary keywords
- Word count recommendation (based on cluster size: 3–5 kw → 1000–1500w; 6–10 kw → 1500–2500w; 10+ kw → 3000w+ pillar)
- Content type: guide / comparison / listicle / review / explainer / roundup
- Proposed URL slug
- H2/H3 outline (full section structure)
- Internal links: which existing pages to link to + which pages should link to this post
- CTA recommendation (what should the reader do next — buy, browse category, contact)
- Suggested images: number, type (product shot / lifestyle / diagram / infographic), alt text formulas
- Schema type: Article / HowTo / FAQPage / Product / Review
- FAQ section: 3–5 questions derived from question-intent keywords in the cluster
- Funnel position: Top / Middle / Bottom of funnel

**Pillar + Cluster architecture:** Identify the top 3–5 highest-volume informational topics. These become pillar posts (3000w+). All related cluster posts link back to the relevant pillar.

**Content calendar:** Sequence blog posts by Tier (T1 first), then by funnel position (Bottom → Middle → Top). Output a 12-week publishing schedule.

---

## Phase 7 — FAQ Bank Generation

→ Read `references/content-planning.md` § FAQ Rules

All question-intent keywords + question signals from across all clusters feed into the FAQ bank.

**FAQ Homepage (6–8 questions):**
- Highest-impact questions only
- Prioritise questions about buying, pricing, shipping, product types
- Each answer: 40–60 words, conversational, includes primary keyword naturally
- Includes JSON-LD FAQPage schema block

**FAQ Page (full bank, grouped by theme):**
- All question keywords organised into thematic sections
- Each answer: 50–80 words, includes 1–2 supporting keywords naturally
- Speakable schema flagged on top answers
- Each answer optimised for featured snippet extraction

**⭐ Page-Level FAQ (every mapped page, not just homepage + FAQ page):** a 2–4 question mini-FAQ on every product/category/brand-hub/blog page that has question-intent keywords in its cluster (or an obvious buyer question even without one — use judgment, don't invent filler). This is the biggest lever for organic keyword coverage in this phase — each page-level FAQ answer is unique indexable content that lets one page compete for query variations it otherwise can't touch, without diluting the page's primary-keyword focus. Skip only when a cluster genuinely has nothing to draw on. Its own FAQPage schema instance per page. Full rules in `references/content-planning.md` § Page-Level FAQ.

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
- Page-level FAQ candidates, pre-drafted for the same reason (2–4 Q&As where the cluster supports it)
- Priority tier (T1 gaps first)

**Separate brand gap vs product gap vs category gap clearly.**

**Competitor Gap (optional — requires a competitor SEMrush export):** if the user provides a competitor's SEMrush Organic Research/Keyword Gap export, cross-reference it against this site's Primary Pool and page inventory to find keywords the competitor visibly ranks for that this site has no coverage for at all. No API access — export only, same as the site's own keyword data. Skip cleanly if not provided. Full workflow in `references/product-gaps.md` § Competitor Gap Analysis.

**Link Magnet Candidates:** once per session, after all gaps are flagged, scan for 1–2 realistic link-worthy content candidates (free tool, original data, resource hub, comparison, downloadable, embeddable widget, digital PR hook) — the on-page lever for earning backlinks and referral traffic, not just search rankings. Quality over volume — state plainly if no strong candidate exists rather than padding the list. Full detail in `references/product-gaps.md` § Link Magnet Candidates.

---

## Phase 9 — AI/GEO/AEO Visibility Layer

→ Read `references/ai-visibility.md`

Run this layer across all outputs — it annotates the keyword map and content plan with AI visibility signals.

**Seven signals applied to every page and blog post:**

1. **FAQ Schema** — every page with 2+ question-intent keywords in its cluster gets a FAQPage JSON-LD block planned
2. **Speakable Schema** — flag the single best FAQ answer on each page for `speakable` schema (voice + AI assistant readability)
3. **Entity Coverage** — check: does each page clearly name the product entity, brand entity, and (where relevant) location entity? Flag gaps.
4. **Featured Snippet Hooks** — every informational/question keyword cluster gets a "definition hook": a 1–2 sentence plain-language answer in the first 150 words of the page
5. **llms.txt Priority Map** — at the end of the session, output a prioritised list of URLs to include in `llms.txt`, ranked by topical authority and AI answer relevance
6. **SERP Feature Targeting** — check the live SERP for the primary keyword (snippet/PAA/image pack/shopping pack) and structure the page to match what's actually showing, instead of one generic format for every page
7. **AI Overview / AI Assistant Citation Optimization** — format the Definition Hook (Signal 4) for AI-citation extraction specifically: fact-first, one claim per sentence, number anchored early, plain-text extractable

**Local Business Schema (situational):** sites with a physical location/service area get `LocalBusiness` schema (address, geo, openingHours, areaServed) on each location page instead of the generic Organization schema — one block per location, never shared. Skip for ship-anywhere ecommerce sites. See `references/ai-visibility.md` § Local Business Schema.

---

## Output Documents

Produce all five documents at the end of every session.
→ See `references/output-formats.md` for exact templates.

| Document | WebForge Uses It For | Contents |
|----------|---------------------|---------|
| `keyword-map.md` | Page meta, H1s, on-page copy | Full keyword allocation table — every keyword assigned to a URL with tier, intent, role |
| `keyword-cluster.txt` | Blog topic queue | Same cluster data in flat, WebForge-readable format — the blog post build queue |
| `blog-plan.md` | Blog post builds — titles, outlines, schema, internal links | Full brief for every planned blog post + 12-week content calendar |
| `faq-bank.md` | Homepage FAQ section + FAQ page build + FAQPage schema | All FAQ Q&As with JSON-LD schema blocks, grouped by theme |
| `product-gaps.md` | Product/category page creation decisions | All product/category/brand gap proposals with full demand analysis |

**⚠️ WebForge Rule 12 — all five documents go in `docs/` only.**
Never place them in `public/` or include them in any deploy ZIP. These are internal strategy files — putting them on the live site hands competitors the entire plan. WebForge enforces this at crosscheck.

**`keyword-cluster.txt` companion file:** Always produce this alongside `keyword-map.md`. It is the same cluster data in the flat format WebForge's project instructions reference. WebForge reads `docs/keyword-cluster.txt` to pull the next unused blog cluster for each new post.

**In-chat summary after each session:**
- Total keywords processed
- Keywords kept vs dropped
- Pages mapped
- Blog posts planned
- FAQ entries generated
- Product gaps found
- AI visibility flags raised
