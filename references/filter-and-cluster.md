# Filter, Intent & Clustering Reference

**Calibrated to SEMrush KD% (0–100 scale).** If a client's export comes from a different tool (Ahrefs KD, Moz, etc.), say so explicitly in the session summary — the numbers below assume SEMrush's difficulty curve and will read too strict/loose against another tool's scale.

## Filtering Rules

### Niche Relevance
Drop a keyword if it has zero semantic connection to the site's niche. Use the niche summary provided at session start.
- Keep: anything about the product type, accessories, related activities, buying signals, brand names in the niche
- Drop: unrelated products, generic terms that could mean anything, irrelevant industries

When in doubt about relevance, keep the keyword and flag it for manual review rather than silently dropping it.

### Volume Floor — intent-sensitive, not flat

A flat floor throws away real money: a "buy [specific product model]" keyword at Vol 25 converts at a far higher rate than a Vol 25 informational term, and dropping it loses genuine revenue. The floor now varies by intent:

| Intent | Volume Floor | Why |
|--------|--------------|-----|
| Transactional | **20** | Low-volume + ready-to-buy is still worth a page — these visitors convert |
| Question | **20** | Low-volume questions still deserve an FAQ answer; the cost of including one is near-zero |
| Commercial | **50** | Needs assured traffic to justify comparison/review content investment |
| Informational | **50** | Needs assured traffic to justify guide/pillar content investment |
| Navigational | **No floor** | Brand/model terms are kept regardless of volume — completeness matters more than volume here |

Below the applicable floor = not worth a dedicated strategy. Drop and count, noting which floor applied.

### KD Ceiling & Pools

Tightened further still — primaries are now hard-capped at KD ≤28, not the old 0–34 band. SEMrush's KD% is known to under-represent true ranking difficulty for smaller/newer sites (it weights backlink profiles of current rankers, not the content depth or authority a new site actually needs). These bands assume a small-to-mid authority ecommerce site, not an established domain.

| KD Range | Pool | Rule |
|----------|------|------|
| 0–28 | ✅ Primary Pool | Can be primary keyword on a dedicated page |
| 29–35 | 🟡 Secondary Fallback Pool | Secondary/LSI use only, **and only when genuinely needed** to hit the secondary minimum — never primary, never a default-use pool |
| 36+ | 🔴 Dropped | Exclude entirely, no exception — not for enrichment copy, not for a later revisit |

**No "High Volume Outlier" exception — removed entirely.** A keyword above KD 35 is dropped regardless of volume, even at Vol 2000+. There is no "Revisit in 6 months" appendix in `keyword-map.md`. Chasing a keyword that takes real authority to rank for isn't worth it even when tempting, high-volume data is attached — this replaces the old exception outright, not alongside it.

**Exception — Low-KD Rescue (the mirror case, unaffected by the tightened ceiling):** a Transactional (Vol < 20) or Commercial (Vol < 50) keyword below its own intent's volume floor from the table above but with **KD ≤ 15** is not dropped — it's genuinely easy to rank for, and T/C intent means it converts when it does. Route it to the **Secondary Fallback Pool**, never as a primary/dedicated-page keyword (the volume alone doesn't justify a whole page), but it's a first-choice pick when supplementing a cluster's secondaries (see Secondary Keyword Supplementation below) — it's real, scored, easy-to-rank data, which beats reaching for a generated or related-search term with no data at all. **KD ≤ 10** specifically is the strongest rescue tier — flag these distinctly (`⭐ rescue`) since they're near-guaranteed quick wins.

### Situational Drop — "Not Worth Fighting For"

The numeric bands above are necessary but not sufficient. Some keywords pass every threshold and still aren't worth the effort *for this specific site, in this specific niche* — KD is a backlink-profile estimate, not a guarantee, and it can't see what's actually sitting in the SERP. Before finalizing the Primary Pool, spot-check the highest-value candidates (T1/T2 keywords the map will actually build pages for) against these situational red flags:

| Red flag | What it looks like | What to do |
|---|---|---|
| **Marketplace-dominated SERP** | Top 5-10 results are Amazon, eBay, Walmart, or similarly huge marketplaces — not independent retailers | Downgrade out of T1/T2 regardless of KD number; a small/new site realistically cannot outrank marketplace listings for this specific query. Keep it as a secondary/LSI term instead of a dedicated-page target. |
| **Non-commercial SERP for a "commercial" keyword** | A keyword tagged Transactional/Commercial actually returns forums, Reddit, YouTube, or Quora in the top results | The labeled intent doesn't match reality — Google isn't reading this as a buying query no matter what the keyword text implies. Don't build a product/category page around it; route it to a blog/informational treatment instead, or drop. |
| **Structurally irrelevant audience** | The keyword is technically on-topic but serves a search population the site doesn't actually sell to (e.g. a rental/hire-focused query on a site that only sells) | Drop, regardless of KD/Volume — the traffic wouldn't convert even if it ranked. |
| **Niche too saturated at this KD** | The niche summary indicates heavy, well-funded competition (large national chains, established DTC brands) even at KD levels that would be easy in a quieter niche | Note as a judgment call in the session summary rather than silently including it — the client should decide whether to chase it anyway. |

**This is a judgment layer, not a rigid rule** — when a red flag is genuinely ambiguous, flag it for the client rather than silently dropping or silently keeping it (same "flag, don't guess" principle as niche relevance above). State which flag applied and why in the keyword-map's notes for any keyword downgraded this way, so the client can see the reasoning and override it if they disagree.

### Deduplication
1. Lowercase everything
2. Exact duplicates → keep one (highest volume wins)
3. Near-duplicates (singular/plural, spelling variants, word order variants) → merge, keep higher-volume form, note the variants as LSI
4. Acronym variants → keep the most-searched form, note the other as LSI

### Brand Contamination
- Competitor brand names → move to "Competitor Brands" list
- These are valid ONLY for comparison/review blog posts (e.g. "Sur-Ron vs KTM electric")
- Never use a competitor brand name as the primary keyword on a product page
- Own brand name keywords → Navigational intent, assign to homepage or brand page

### Geography Filter
Apply strictly per site:
- **US sites:** keep US spelling (aluminum, tire, gas), US units (mph, inches), US brand availability
- **UK sites:** keep UK spelling (aluminium, tyre, petrol), UK units (mph but metric optional), UK brand availability
- Drop any keyword that clearly targets the wrong market
- Ambiguous keywords (no clear market signal) → keep for both but note as "market-neutral"

---

## Intent Classification Rules

**⭐ Tie-break rule (apply first, always):** many real keywords carry signal words from more than one category — "how much does it cost" has both `how much`/`cost` (Transactional) and `does` (Question); "is it worth it" has both `worth it` (Commercial) and `is it` (Question). When a keyword matches signals from two or more categories, the higher-priority category always wins — never split the difference or classify by "which signal appears first in the string." Fixed order:

**Transactional → Commercial → Informational → Question → Navigational**

Worked examples: `buy [brand] [model]` matches Transactional (`buy`) AND Navigational (brand+model) → classify Transactional, it wins. `best [product] review` matches Commercial (`best`, `review`) only → Commercial. `how much does [product] cost` → Transactional (`how much`, `cost` outrank `does`). `is [product] worth it` → Commercial (`worth it` outranks `is it`).

### Transactional (highest priority)
**Signals:** buy, for sale, price, cost, how much, cheap, deal, discount, order, shop, near me, free shipping, in stock, purchase, get, where to buy
**Assign to:** product pages, category pages
**Never assign to:** blog posts (you'll bury the conversion opportunity)

### Commercial (second priority)
**Signals:** best, top, review, recommended, vs, compare, worth it, pros cons, alternatives, ranked, [year] + product, honest review
**Assign to:** blog posts (comparison/review type), category pages if volume justifies
**Note:** "Best electric dirt bikes" → category page if you carry multiple brands; blog post if it's editorial

### Informational (third priority for primary-page assignment, LAST priority for blog sourcing)
**Signals:** how to, what is, why, guide, tips, explained, tutorial, learn, beginners, complete guide, everything you need to know
**Assign to:** blog posts (guides, pillar content) — **reversed from the original release: blog posts are NOT anchored on Informational by default.** The sourcing order is strict: Transactional (true orphans, vol 20–99 — "Reason A," see Orphan Keywords below) → Commercial → Informational, with Informational as last-resort filler only once T/C are exhausted. Informational is never the pillar/guide backbone on its own — see `page-mapping.md` §7 for the full Reason A/B routing.
**Note:** High-volume informational keywords = pillar post candidates, but only sourced after the Transactional/Commercial pool for this batch is exhausted

### Question Intent
**Signals:** does, can I, is it, how long, will, should, do I need, what happens, how often, are there, is there
**Assign to:** FAQ bank (homepage FAQ, the dedicated FAQ page, AND a page-specific mini-FAQ on every product/category/individual-brand/Brand-Hub/shop/blog/active-Sale/Best-Sellers/New-Arrivals/Compare/Wholesale page where relevant question-intent keywords exist — see content-planning.md § Page-Level FAQ)
**Secondary use:** include as H2 questions within relevant blog posts

### Navigational
**Signals:** brand name alone, brand + model number, brand + site name
**Assign to:** Individual Brand pages, individual product pages — **Individual Brand pages are anchored on Navigational primary keywords by default.** (Not to be confused with the separate aggregator "Brand Hub" page — see `page-mapping.md` §9 — which only exists once a site stocks 3+ brands and is anchored Informational/Navigational as a directory, not per-brand.) A brand page whose primary keyword isn't a brand/navigational term has drifted from its job.
**Note:** If you don't stock the brand yet → product gap flag

### Local Intent Layer (situational — only for sites with a physical location or service area)

**Skip entirely for a pure ecommerce/ship-anywhere site** — this only applies when the niche summary or site scan shows a physical location, showroom, service area, or local delivery/installation offering.

**Signal:** "near me," a named city/region + product/service, "[service] in [city]," "local," "delivery to [area]."

**Handling:**
- Tag these Transactional (they already carry buying intent, "near me" is a modifier on top, not a separate intent category)
- Cluster separately from the site's general commercial/transactional clusters — a "[product] near me" or "[product] in [city]" cluster maps to a dedicated location/service-area page, never bolted onto the general category page as a secondary
- If the site has multiple physical locations, each gets its own location-page cluster — don't merge them, that's the cannibalisation rule applying at the location level same as anywhere else
- Route to LocalBusiness schema in the AI/GEO layer (`references/ai-visibility.md`) rather than the generic Organization schema

**On-page requirement (location pages specifically):** NAP (Name/Address/Phone) consistency, embedded map, service-area description, local-specific FAQ (opening hours, parking, local delivery radius) — these are location-page-specific additions on top of the normal on-page formula, not a replacement for it.

---

## Scoring Rules

### Priority Tier Assignment
After intent classification, assign every Primary Pool keyword a tier. Volume floor is intent-sensitive (see Filtering Rules above — 20 for Transactional/Question, 50 for Commercial/Informational). **Tier applies to the primary keyword only — nothing above KD 28 is ever a primary, no fallback:**

| Tier | KD | Expected Rank Time | Priority |
|------|-----|-------------------|----------|
| T1 🥇 | 0–19 | 1–3 months | Highest — build first |
| T2 🥈 | 20–28 | 2–4 months | High — build with quality content |
| Secondary Fallback (no Tier) | 29–35 | N/A — never primary | Secondary/LSI only, used only when needed to hit the secondary minimum |

T1 is deliberately tighter than a generic "0–25" band — for a newer/smaller site, genuine 1–3-month wins live closer to KD 0–19 on SEMrush's scale. T2 narrowed from the original 20–34 down to 20–28 (rank-time estimate tightened to 2–4 months accordingly) — nothing above 28 can be a primary, ever, even as a last resort.

### Opportunity Score (for ranking within a tier, and for picking which keyword becomes primary in a cluster)

Replaces the old volume-only composite score. Folds in CPC — a collected-but-previously-unused signal — as a real value indicator: a keyword with a $3 CPC represents buyers worth more per visit than a $0.20 CPC keyword at the same volume, and should be prioritized accordingly for "clean choices," not just easy ones.

```
Score = ((Volume × Intent Weight) / 10) − (KD × 2) + (CPC × 3)
```

**Intent Weight:** Transactional ×1.5 · Commercial ×1.2 · Question ×1.1 · Informational ×1.0 · Navigational ×1.0

Higher score = higher priority. Use this to:
- Rank keywords within the same tier when several compete for one assignment slot
- Pick the primary keyword within a cluster (replaces the old "highest volume, lowest KD" rule alone — now highest Opportunity Score, which already accounts for both plus intent and commercial value)
- Order the Top 5 Priority Actions in the session summary

If a keyword's export has no CPC column, treat CPC as 0 for that keyword (the formula degrades gracefully — it just stops rewarding commercial value it has no data for, rather than breaking).

### Primary/Secondary Intent Priority (site-wide, on top of Opportunity Score)

**Primary keyword selection priority: Transactional first, Commercial second.** This gates which intent pool the Opportunity Score formula is even allowed to draw from — it doesn't replace scoring, it restricts it. First filter candidates to Transactional-only (among those that already passed the Filtering Rules above); if one or more qualify, rank *within that Transactional-only pool* by Opportunity Score to pick the actual primary. Only if zero Transactional candidates qualify does the pool open up to Commercial candidates, scored the same way. The Intent Weight in the Opportunity Score formula already favors Transactional (×1.5) over Commercial (×1.2), but that's a soft scoring bias — this gate is a hard restriction on which pool is even eligible, and it's what actually enforces Rule 2 (the aim is sales) at the point where a primary keyword gets picked.

- **This priority can never override the Filtering Rules or Situational Drop.** A Transactional keyword that failed a situational-drop check (e.g. marketplace-dominated SERP) doesn't count as "available" just because it's nominally Transactional — Commercial still wins in that case.
- **Low-KD Rescue keywords remain secondary-only, never primary** — unaffected by this rule. T-priority governs selection among keywords that already qualify as viable primaries; it never promotes a rescue-only keyword past that restriction.
- **Secondary keyword selection priority: Commercial first, Transactional second** — the inverse order from primary. A page's primary leans Transactional, its secondaries lean Commercial, with Transactional secondaries filling any remaining gap.
- Availability-dependent, not a mandate: if the preferred intent genuinely isn't available for a given page, fall through to the next intent in order rather than forcing a bad fit.
- **Carve-out:** Individual Brand pages (`page-mapping.md` item 2, "Individual Brand pages specifically") still anchor on **Navigational** primaries regardless of this rule — not to be confused with the Brand Hub aggregator (item 9), which anchors Informational/Navigational as a directory. This T/C priority rule governs commercial/shop/category pages, not either of these.
- **Homepage and the top-level shop page specifically must prioritize Transactional intent for their primary keyword** — stronger than the general rule above, and identical for both pages since they carry equal importance (`page-mapping.md` item 3, "Homepage AND Top-Level Shop Page"). The eligible-primary rule there allows "brand term OR top commercial term"; this tightens it toward Transactional specifically when a qualifying candidate exists.

---

## Clustering Rules

### Seed Clusters (only when Phase 0 ran — `niche-taxonomy.md`)

**If `niche-taxonomy.md` produced a `taxonomy-map.md`, every category/subcategory in it becomes a seed cluster before clustering below runs.** Check each natural cluster against the seed clusters first: a topical match joins (extends) the existing seed cluster rather than forming an independent one; this is what keeps a category page's keyword set coherent with the taxonomy it's supposed to represent. A cluster with no match goes through the ordinary clustering process below — if it's strong enough to need its own page but has no taxonomy home, it surfaces as a normal Category Gap (`page-mapping.md`'s New Category Page flag), not a separate mechanism. Skip this subsection entirely when no Phase 0 run exists for this project (the normal case when the user supplied a keyword/product list directly).

### What Makes a Cluster
A cluster is a group of keywords that should all be targeted by a single URL. Test: "Would a user searching any of these keywords be satisfied by the same page?" If yes → same cluster.

### Cluster Size (raw clustering stage — before page-assignment finalization)
- Minimum: 2 keywords (singles go to orphan review list)
- Maximum: 15 keywords (split larger clusters by subtopic)
- Sweet spot: 4–8 keywords per cluster

This is the size of the *natural* cluster formed from the pasted export. It's allowed to be thin at this stage — the minimum secondary requirement below is enforced later, at page-assignment (Phase 5), after supplementation.

### Keyword Roles Within a Cluster (final, page-ready state)
| Role | Count | Criteria |
|------|-------|---------|
| Primary | Exactly 1 | Highest Opportunity Score in the cluster (see Scoring Rules) |
| Secondary | **Minimum 5, maximum 8** | Closely related, same intent as primary, page-worthy |
| LSI/Supporting | Unlimited | Semantically related, Secondary Fallback (KD 29–35) keywords welcomed here |

**⭐ Every page-mapped cluster must reach 1 primary + 5+ secondary before the keyword-map is finalized.** This is a hard floor, not a target — a page shipping with only 2–3 secondary keywords is under-optimized and won't compete for the breadth of queries it should. Homepage AND the top-level shop page are the two exceptions, treated identically (see page-mapping.md — lighter treatment, topical-dilution risk is real on the site's two highest-authority pages).

### Secondary Keyword Selection Rules

Not every topically-related keyword is a valid secondary — apply these before adding one to a cluster:

1. **Intent compatibility with the primary.** A secondary should share the primary's intent, or be Question-intent (which supports any primary via the page-level FAQ, see content-planning.md). Never attach a purely Informational secondary to a Transactional-primary product page, or a Transactional secondary to a pure guide/pillar post — it signals the wrong thing to both the reader and Google about what the page is for. Commercial secondaries are compatible with a Transactional primary (e.g. a product page can carry a "best" comparison-flavoured secondary) since they still point at the same buying decision.
2. **Same topic, real modifier variance.** A secondary should be the same product/topic as the primary, differentiated by a real modifier (price angle, use-case, audience, format) — not just a synonym restatement of the primary.
3. **Page-worthy, not filler.** A secondary must be something the page can genuinely satisfy in its own content (a heading, a paragraph, a spec row) — if a keyword doesn't fit anywhere real on the page, it belongs in LSI/Supporting instead, not forced into the secondary slot just to hit a count.
4. **Low-KD Rescue keywords get priority.** A real, scored Transactional/Commercial keyword at KD ≤ 15 (see the Low-KD Rescue exception above) always beats a generated or related-search secondary with no data behind it — use these first when supplementing (see step 1 below).

### Secondary Keyword Supplementation (when the natural cluster is thin)

If the raw cluster has fewer than 5 candidate secondaries after clustering, build up to 5 in this order — stop as soon as you hit 5, but note the last source actually used so the map stays honest about where each keyword came from:

0. **Site-search query mining (if a site-search export is provided) — the highest-priority source when available.** If the user has internal site-search logs (most ecommerce platforms — Shopify, WooCommerce, etc. — can export this), pasted as a Query/Count list, check it for terms matching the cluster's topic. This is first-party, real-user intent data on this exact site and audience — stronger evidence than a generic SERP related-search, which only shows what's generically associated with the topic across the whole web. Optional input, skip cleanly if not provided (see Phase 1 startup).
1. **Broaden within the existing pools first — Low-KD Rescue keywords first, then the rest of the Secondary Fallback/Primary Pool.** Re-scan for real, data-backed keywords on the same topic that didn't cluster tightly enough to be picked up automatically, prioritizing any KD ≤ 15 rescue candidates (⭐-flagged) before other Secondary Fallback Pool terms. This is real search data — always prefer it over generated keywords.
2. **Competitor keyword mining (if a competitor SEMrush export is provided).** Scan the competitor's Organic Research/Keyword Gap export (the same one used for Competitor Gap Analysis, `references/product-gaps.md`) for real keywords on the same topic that the competitor ranks for and this site hasn't already claimed elsewhere. This carries real Volume/KD/CPC data, same as the site's own export — just from a different domain's ranking profile — so it outranks the no-data sources below it. Run every candidate through the normal Phase 1 filters (volume floor, KD ceiling) before use; a competitor ranking for a KD 70 term doesn't make it a valid secondary here any more than it made it a valid gap in Phase 8. Optional, skip cleanly if no competitor export was provided.
3. **Google related searches.** `web_fetch` the live Google SERP for the cluster's primary keyword and pull the "related searches" / "people also ask" / "searches related to" terms shown. These are real query patterns Google itself associates with the topic, even without a volume number attached.
4. **Generated transactional modifiers.** Combine the cluster's core topic noun with standard commercial modifiers to fill any remaining gap: `buy [X]`, `[X] for sale`, `cheap [X]`, `[X] price`, `[X] near me`, `shop [X] online`, `order [X]`, `[X] deals`, `best price on [X]`. Use only the modifiers that fit the cluster's actual intent — never bolt `buy`/`for sale` onto a purely informational cluster.

**Label site-search-sourced keywords `[site-search]`** in the output, same as `[competitor]`/`[related-search]`/`[generated]` — they carry real query-count data (treat the query count as a rough volume proxy, not a SEMrush-equivalent number) but aren't from the original SEMrush export either, so the source stays transparent.

**Scoring supplemented keywords:** keywords added via steps 0, 3, and 4 have no real SEMrush Volume/KD/CPC data (step 0's site-search query count is a usage signal, not a SEMrush-equivalent score). All three **inherit the cluster's Tier** (T1/T2, same as the primary keyword) as a labeling convenience rather than being scored independently — simpler and faster than requiring separate verification, but it does mean the tier assignment for these specific terms is an assumption, not measured data. Steps 1 and 2 are the exception — both carry real SEMrush Volume/KD/CPC data (the site's own export and the competitor's export respectively) and are scored normally via the Opportunity Score formula, which means they follow the actual KD-based Tier rule from that data rather than inheriting: no Tier label at all if the real KD lands in the 29–35 Secondary Fallback band — real data doesn't earn an exception from that rule.

**Label the source.** In the keyword-map output, mark every supplemented keyword with its source tag — `[site-search]`, `[competitor]`, `[related-search]`, or `[generated]` — next to the keyword, so a client reading the map can see at a glance which secondaries are export-backed and which were added to reach the floor.

**Never pad with irrelevant keywords.** If a cluster is genuinely so niche that even related-searches + generated modifiers can't reach 5, ship it honestly — e.g. "Secondary count: 3/5 — niche too narrow for more, no forced padding" — rather than inventing keywords with no real connection to the page.

### Cannibalisation Rules
- One cluster = one URL. Non-negotiable.
- If two clusters would logically land on the same URL → merge them
- Never split a topic across two pages hoping to "cover more ground" — it splits authority
- Check: if Google would show the same page in results for two different clusters, those clusters must be merged
- **This applies to secondaries too, not just primaries.** Maintain a running used-keyword registry across every cluster as you assign secondaries — including supplemented ones (`[site-search]`, `[competitor]`, `[related-search]`, `[generated]`, Low-KD Rescue) — and never let the same keyword serve as a secondary on two different pages. Full audit procedure in `references/page-mapping.md` § Cannibalisation Audit.

### Cluster Naming
Name each cluster by its primary keyword for clarity. This name is used throughout all output documents.

### Orphan Keywords
Single keywords that don't cluster with anything:
- If transactional/commercial + Vol 100+ → create a minimal cluster (this keyword as primary) and run it through Secondary Keyword Supplementation above to reach the 5+ floor before mapping it to a page
- **If Transactional + Vol 20–99 ("Reason A" — true orphan, too low volume for its own page) → blog-eligible**, per the reversed blog-anchoring rule above. **Carve-out:** never applies if the keyword is actually the intended primary of a real taxonomy category, the homepage/shop page, the FAQ page, an active Sale/Best Sellers/New Arrivals/Compare/Wholesale page, an already-stocked product, or a stocked brand/Brand Hub — in those cases that page type's own rule takes precedence, full stop. Full routing in `page-mapping.md` §7.
- **If Informational + Vol < 200 ("Reason A2" — true orphan, too low volume for its own page) → blog-eligible**, sourced as Informational last-resort filler per the strict T→C→I blog sourcing order (never ahead of Reason-A Transactional or Commercial), not dropped to a separate holding list. **Carve-out:** same as Reason A — never applies if the keyword is actually the intended primary of a real taxonomy category, the homepage/shop page, the FAQ page, an active Sale/Best Sellers/New Arrivals/Compare/Wholesale page, an already-stocked product, or a stocked brand/Brand Hub.
- If question-intent → route directly to FAQ bank regardless of whether it clusters
