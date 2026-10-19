# Page Mapping Reference

## Site Scan Protocol

### If a URL is provided
Use web_fetch on the homepage. Extract:
- Site title and meta description
- Main navigation links (these reveal the site's primary categories)
- Any product/category/brand names visible
- Blog section URL if present
- Footer links (often reveal full site structure)

Then fetch 2–3 key inner pages (e.g. a main category, a product page) to understand URL pattern and page structure.

Build a working page inventory:
```
URL | Page Title | Page Type | Current H1 (if visible)
```

### If a page list is pasted
Use it directly. Ask the user to confirm the page types if not obvious from the URLs.

### If neither is provided
Ask before proceeding. Page mapping without site context produces generic, unusable output.

---

## Mapping Priority Order

Apply this strict priority when deciding where a cluster goes:

### 1. Existing Product Page
**Condition:** Cluster primary keyword matches a specific product the site already sells
**Action:** Assign cluster to that product page URL
**On-page notes:** Add primary keyword to title tag, H1, meta description, first paragraph, and at least one image alt text. Secondary keywords go in H2s, product description body, and spec table if present.

### 2. Existing Category or Brand Page
**Condition:** Cluster primary keyword is category-level (covers multiple products) or brand-level (a brand the site stocks)
**Action:** Assign to existing category/brand page
**On-page notes:** Primary keyword in title tag and H1. Secondary keywords in intro paragraph, filter labels, subcategory headings. LSI keywords in product card descriptions.

**Individual Brand pages specifically: anchor on Navigational.** (This file previously called these "brand hub pages" — renamed here to avoid colliding with the separate, new aggregator page in #9 below, which is now called "Brand Hub.") An individual brand page's primary keyword should be the brand-navigational term (`[Brand]`, `[Brand] UK`, `[Brand] official`) per the Intent Classification tie-break rule in filter-and-cluster.md — not a generic category or commercial term that happens to mention the brand. If a brand-page cluster's primary keyword isn't actually navigational, either the page isn't a true individual brand page or the primary keyword needs re-picking. Category pages (not brand-specific) follow the normal Commercial/Transactional anchoring instead.

### 3. Homepage AND Top-Level Shop Page — lighter treatment, on purpose, both equally
Both pages get identical priority and treatment — equal importance, not homepage-first. They're kept as one numbered item because the reasoning and shape are shared; each still gets its own distinct primary (see cannibalisation note in 3B).

**Rule: Exactly 1 primary keyword (highest-Opportunity-Score brand/top-level commercial term) + 3–5 secondary/LSI keywords, for EACH of homepage and shop page.** Deliberately lighter than the 1 primary + 5+ secondary floor every other page carries.

**KD ceiling — stricter than the general rule, no exceptions.** Both pages' primary AND secondaries must be **KD <28, full stop** — not the ordinary ≤28-with-35-fallback that other pages get. If secondaries can't reach the target count within <28, ship honestly with fewer rather than reaching into the fallback band.

**Why the exception:** these are the site's two highest-authority pages — the ones Google shows for brand searches and broad catalog-entry searches. Forcing the full product-page-level breadth of 5+ secondary long-tail targets onto either risks (a) topical dilution — a focused page ranks better than a scattered one, (b) reading like a keyword-stuffed listicle rather than a clean hub, and (c) cannibalizing the category/product pages that should rightfully own those long-tail terms.

#### 3A. Homepage
**Eligible primary:** brand-level term or the single highest-volume top-level commercial keyword (e.g. "electric dirt bikes UK").
**Eligible secondaries:** brand name variations, top category umbrella terms (not deep long-tail modifiers — those belong on their own dedicated product/category pages, never stuffed onto the homepage). Do not run homepage secondaries through the Google-related-search / generated-transactional-modifier supplementation process used elsewhere — homepage secondaries should stay close to the primary, not padded out to a count.
**On-page notes:** Homepage is a hub — keywords should appear in hero headline, intro paragraph, section headings, and meta description. Do not force product-specific keywords onto the homepage.
**Feeds the `knowsAbout[]` schema field** (ai-visibility.md's Organization schema) alongside the shop page below — no separate tracking, this is a read off the primary+secondaries already assigned here.

#### 3B. Top-Level Shop Page
**Eligible primary:** the broad catalog-entry Transactional query — e.g. "shop [niche] online," "buy [niche] products" — the aggregator-level buying intent, distinct from whatever the homepage's primary ends up being.
**Eligible secondaries:** same discipline as the homepage — stay close to the primary, no padding-to-a-count supplementation process.
**On-page notes:** same formulas as homepage (hero headline, intro paragraph, section headings, meta description), applied to the shop page's own catalog-entry framing rather than the brand framing.
**Distinctiveness from the homepage.** The shop page and homepage must be substantively distinct, not just technically different URLs sharing near-identical keywords — if both end up contesting the same best keyword, the same Opportunity-Score tie-break used throughout the Cannibalisation Audit below decides which keeps it; the other takes its next-best qualifying keyword.
**Feeds the `knowsAbout[]` schema field** too, alongside the homepage — a second designated source feeding the same array, not a separate field.

### 4. Existing Blog Post
**Condition:** Cluster is informational/commercial AND a directly relevant blog post already exists
**Action:** Assign cluster to improve that post (add a content refresh flag)
**On-page notes:** Flag specific sections where keywords should be added or headings updated

### 5. New Product Page (Gap Flag)
**Condition:** a cluster (Transactional OR Commercial — the gap-type mapping isn't rigidly tied to intent) with no matching product on the site
**Action:** Flag as product gap → route to product-gaps.md's full build criteria (KD/intent/price-tiered-volume, with a pre-built keyword package that makes an approved gap instantly publishable)
**Include:** Proposed URL slug, proposed page title, primary keyword, all cluster keywords

### 6. New Category Page (Gap Flag)
**Condition:** a cluster for a product category the site doesn't have a page for
**Action:** Flag as category gap → route to product-gaps.md. **An approved category (or brand) gap now cascades into its own starter-product-research pass** before it ships — it launches with real, keyword-assigned products queued, not just a bare category name.
**Include:** Proposed URL, proposed title, primary keyword, which existing products would belong here

### 7. New Blog Post
**Condition:** a missing page has three different causes, and only two of them mean "blog it" — this is not just "no existing page match":
- **Reason A — true orphan, too low volume.** A Transactional keyword that never clustered with anything and falls at volume 20–99 (below the orphan threshold of 100 that would otherwise earn its own minimal cluster/page). **Carve-out:** never applies to a keyword that's actually the intended primary of (a) a real taxonomy category/subcategory, (b) the homepage or shop page, (c) the FAQ page, (d) an active Sale/Best Sellers/New Arrivals/Compare/Wholesale page, (e) a product already in the stock list, or (f) a brand the site actually stocks (its Individual Brand page) or the Brand Hub when it's active (3+ brands) — in every one of these cases, that page type's own rule takes precedence, full stop.
- **Reason A2 — Informational orphan, too low volume for its own page.** An Informational keyword that never clustered with anything and falls below volume 200. Same shape as Reason A, same carve-out (a)–(f) applies — never blog-routed if it's actually the intended primary of a Guarantee-driven or active page. Blog-eligible, but sourced strictly as last-resort filler (see sourcing order below), never ahead of Reason-A Transactional or Commercial, and never a separate holding list.
- **Reason B — no matching product/category exists.** Real volume, but the site doesn't stock a matching item or carry that category. This is an inventory problem, not a content one — **always routes to a Gap Flag (#5/#6 below), never to blog**, regardless of volume. Burying a "client should stock this" signal inside a blog post hides a sales opportunity instead of capturing one.

**Action (Reason A/A2 only):** Route to blog planning → becomes a blog brief in blog-plan.md.

**Sourcing order — confirmed override of the old Transactional-on-blog ban, strict order:**
1. **Transactional keywords (vol 20–99, Reason A only)** → blog post topics. A real, buyer-intent search term too low-volume for its own page, captured via blog content instead of wasted.
2. **Commercial keywords (vol ≥20)** → blog comparison/review content.
3. **Only once T+C are fully exhausted** → fall back to Informational for blog primaries (including Reason-A2 orphans), as last-resort filler to keep batches full — not a parallel/equal content type and never the backbone. (Reversed from the previous "anchor on Informational" rule — that is no longer correct.)

### 8. Programmatic Pattern Pages (Scale Catalogs Only)
**Condition:** the catalog has a genuine combinatorial structure — the same modifier (size, color, brand, use-case, price-band) applies across many products/categories in a repeatable pattern (e.g. `[Brand] × [Category]`, `[Size] × [Product Type]`, `[Use-case] × [Category]`) — and the keyword data shows real, non-trivial search volume for enough of the individual combinations to justify dedicated pages rather than filters.
**Action:** Flag as a programmatic page set, not individual one-off gaps. Propose a single URL/template pattern and page-content template (which fields vary, which stay fixed) rather than writing 50 near-identical gap proposals.
**When NOT to use this:** if only 2-3 combinations have real volume, or if the "combinations" don't actually differ enough to avoid duplicate/thin content — those stay as individual product/category gaps instead. This section exists for genuine scale (dozens+ of real, distinct, search-worthy combinations), not as an excuse to mass-produce thin pages.

**On-page notes:** Each generated page still needs a real primary keyword (the specific combination) + the same 5+ secondary floor as any other page — a programmatic pattern describes how the page *template* is built, it doesn't exempt any individual page from the normal keyword-mapping rules. Flag the shared template elements (title tag formula, H1 formula) once, and the per-combination variable data (which specific brand/size/category fills the template) as a data table rather than repeating full prose for each one. **Every generated combination page still runs through the Cannibalisation Audit below** — a shared secondary pool across dozens of near-identical combination pages is exactly the situation the Secondary-level registry check exists for; don't treat programmatic pages as a shortcut around it.

**Output format:**
```markdown
## Programmatic Page Set: [Pattern Name, e.g. "Brand × Youth Category"]

**URL Pattern:** /[category]/[brand]/ (or as fits the site's existing URL structure)
**Combinations with real volume:** [n] of [n possible] — list or attach as a data table
**Title Tag Template:** [Brand] [Category] — [Modifier] | [Site Name]
**H1 Template:** [Formula with variable slots]
**Shared secondary keyword pool:** [keywords that apply across every page in the set]
**Per-combination unique secondary requirement:** each page still needs its own combination-specific secondaries to avoid duplicate content — flag which existing pool keywords apply and where supplementation (filter-and-cluster.md) is needed per combination
**Combinations table:**
| Combination | Primary Keyword | Vol | KD | Priority |
|-------------|-----------------|-----|-----|---------|
| [Brand A + Category X] | [keyword] | [v] | [k] | T1 |
```

### 9. Other Guaranteed/Conditional Page Types
Brief placement rules for page types that don't fit the flow above — full detail is being finalized in the keyword-research workflow and will expand here at that merge; this is enough to map correctly today.
- **FAQ Page — guaranteed default, not conditional.** Every build gets one. Question-intent, not T/C/I — shaped as a comprehensive Q&A bank, never forced into a primary+secondary cluster count.
- **Sale/Deals, Best Sellers/New Arrivals, Compare, Wholesale — all conditional, built only when the client's data/business model actually supports them.** Ordinary-page KD/volume/intent rules apply to each. Sale/Deals and Best Sellers/New Arrivals both carry a cannibalisation check against the homepage/shop, category pages, and each other when both are active.
- **Brand Hub — a separate, new aggregator page, not to be confused with #2's "Individual Brand pages."** Built by default only once the site stocks 3+ distinct brands; skipped entirely below that, not left "conditional-pending." Anchored Informational/Navigational (funnels into individual Brand pages), lighter treatment like the shop page.
- **Individual Brand pages — anchored Navigational** (see #2 above, "Individual Brand pages specifically"), one per brand the site actually stocks.
- **Utility pages (Contact/About/Shipping-Returns vs. Privacy/Terms/Cart/Search/404) — light-touch or fully excluded from keyword targeting respectively.** Never force a cluster onto these.

---

## On-Page Requirements Per Mapped Page

For every cluster-to-page assignment, output these on-page requirements:

### Title Tag Formula
`[Primary Keyword] — [Modifier/USP] | [Brand Name]`
- Max 60 characters
- Primary keyword must appear first or within first 4 words
- Modifier examples: "Buy Online", "Free Shipping", "Official Store", "Complete Guide", "UK's #1"

### H1 Formula
`[Primary Keyword] [Complementary Phrase]`
- Max 70 characters
- Must match search intent (transactional H1 ≠ "Welcome to our store")
- Transactional: "Buy [Product] Online — [USP]"
- Commercial: "Best [Product] in [Year] — Reviewed & Ranked"
- Informational: "How to [Action]: Complete Guide for [Audience]"

### Meta Description Formula
`[Primary Keyword] [value proposition]. [Secondary keyword signal]. [CTA].`
- 145–160 characters
- Must include primary keyword in first 20 words
- Must end with a call to action
- Example: "Shop the best electric dirt bikes for kids. Free UK shipping on all orders over £99. Browse our full range today."

### Image Alt Text Note
`[Primary keyword] — [product detail or context]`
- Example: "electric dirt bike for kids — red 36V youth model"
- Every page should have at least one image with the primary keyword in alt text

### Internal Link Slots
For each mapped page, identify:
- 2–3 pages this page should LINK TO (products → categories; categories → pillar blog posts)
- 2–3 pages that should LINK HERE (blog posts that mention this product/category)

### Page-Level FAQ Note
**Every mapped page — product, category, individual brand, Brand Hub, shop, blog, active Sale/Best Sellers/New Arrivals/Compare/Wholesale — gets a page-specific mini-FAQ (2–4 Q&As) where the cluster has question-intent keywords to draw on, not just the homepage and the dedicated FAQ page.** This is a real organic-traffic lever, not decoration: each FAQ answer is indexable content that can absorb a secondary or LSI keyword naturally, so a page with a mini-FAQ competes for more query variations than the same page without one. Full rules, sourcing, and the "where possible" scope (some thin clusters genuinely have no question-intent keywords to draw on — don't invent questions) are in `references/content-planning.md` § Page-Level FAQ.

---

## Multi-Market / hreflang Note (situational — only if the site serves more than one market)

**Skip entirely for a single-market site (the normal case this skill assumes).** Only relevant if the client explicitly says the site serves more than one country/language from the same domain structure (e.g. a US site adding a UK/CA version, or a bilingual site).

If it applies:
- Each market gets its own keyword session in this skill (**one site = one session** already governs this — a second market is effectively a second "site" for keyword-mapping purposes, run separately, never blended into one keyword-map.md)
- Flag which pages need `hreflang` alternates once both markets' keyword-maps exist, so WebForge can wire the tags between the matching URLs
- Do not assume a keyword translates 1:1 in volume or intent across markets — US and UK volume/KD/competition for the "same" product can differ substantially; treat each market's export as its own dataset, not a shared one with a language swap

This is a lightweight pointer, not a full workflow — most builds are single-market and this section won't apply.

---

## URL Slug Rules

When proposing new URLs:
- Lowercase, hyphenated, no underscores
- Include primary keyword in slug
- Keep under 60 characters total
- No dates in URLs (blog posts included — content stays evergreen)
- Structure examples:
  - Product: `/electric-dirt-bikes/sur-ron-light-bee-x/`
  - Category: `/electric-dirt-bikes/youth/`
  - Brand: `/brands/sur-ron/`
  - Blog: `/blog/best-electric-dirt-bikes-for-kids/`
  - FAQ: `/faq/`

---

## Cannibalisation Audit

**Continuous, not a one-time pass at the end.** Every phase checks the Used-Keywords Registry in keyword-map.md **before finalizing any keyword**, catching a collision as it would happen rather than after the whole map is built — this is a phase-by-phase discipline, never a batch write/check saved for the end. The three levels below are the shape of that check; run them as you go, and treat a final pass over all three as a last confirmation that nothing slipped through, not the first time cannibalisation gets checked.

### 1. URL-level (primary keywords)
- List all assigned URLs
- Flag any URL that has been assigned more than one cluster
- If two clusters land on the same URL: merge them immediately

### 2. Secondary-level (the new risk — check this explicitly)
- Build a running registry of every secondary keyword used across every mapped page **as each page is mapped**, not just at the end
- Before assigning ANY keyword as a secondary — real, Low-KD Rescue, `[site-search]`, `[competitor]`, `[related-search]`, or `[generated]` — check it isn't already a secondary (or primary) on a different page
- If a candidate is already used elsewhere, skip it and take the next candidate in the Secondary Keyword Supplementation order instead — never let the same secondary quietly serve two pages, even a generic generated one like "buy [product]" that's tempting to reuse across similar products
- Two pages should never be trying to rank for the same secondary any more than they should for the same primary — it splits relevance the same way

### 3. FAQ-level
- Build a running registry of every FAQ question used anywhere on the site — homepage FAQ, the dedicated FAQ page, and every page-level mini-FAQ
- If the same buyer question is genuinely relevant to two pages, it gets answered on exactly ONE of them (the best-fit page) — the other pages link to it rather than duplicating the Q&A content
- This applies across all three FAQ locations, not just "page-level FAQ vs homepage/FAQ page" — a page-level FAQ can also collide with another page-level FAQ

Output a clean "no cannibalisation confirmed — URL, secondary, and FAQ levels" note if all three pass clear.

---

## Mapping Output Table Format

**KD reminder: Tier applies to the primary keyword only, and no primary ever exceeds KD 28** (T1 0–19, T2 20–28 — nothing higher, no fallback for a primary). A secondary may extend to the 29–35 band only when needed to hit the secondary minimum; that fallback has no Tier label of its own.

```
| Cluster Name | Primary KW | Vol | KD | Tier | Intent | Assigned URL | Page Type | Status |
|-------------|-----------|-----|-----|------|--------|-------------|----------|--------|
| Youth electric dirt bikes | electric dirt bikes for kids | 1300 | 22 | T1 | Transactional | /electric-dirt-bikes/youth/ | Category | Existing |
| Sur-Ron Light Bee review | sur-ron light bee x review | 480 | 26 | T2 | Commercial | /blog/sur-ron-light-bee-review/ | Blog | New |
```
