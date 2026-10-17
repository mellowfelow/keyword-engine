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

**Brand hub pages specifically: anchor on Navigational.** A brand hub's primary keyword should be the brand-navigational term (`[Brand]`, `[Brand] UK`, `[Brand] official`) per the Intent Classification tie-break rule in filter-and-cluster.md — not a generic category or commercial term that happens to mention the brand. If a "brand page" cluster's primary keyword isn't actually navigational, either the page isn't a true brand hub or the primary keyword needs re-picking. Category pages (not brand-specific) follow the normal Commercial/Transactional anchoring instead.

### 3. Homepage — lighter treatment, on purpose
**Rule: Exactly 1 primary keyword (highest-Opportunity-Score brand or top-level commercial term) + 3–5 secondary/LSI keywords.** This is deliberately lighter than the 1 primary + 5+ secondary floor every other page carries.

**Why the exception:** the homepage is the site's single highest-authority page and the one Google shows for brand searches. Forcing the full product-page-level breadth of 5+ secondary long-tail targets onto it risks (a) topical dilution — a focused page ranks better than a scattered one, (b) reading like a keyword-stuffed listicle rather than a clean brand hub, and (c) cannibalizing the category/product pages that should rightfully own those long-tail terms. A tighter homepage and well-optimized category/product pages perform better together than one overloaded homepage.

**Eligible primary:** brand-level term or the single highest-volume top-level commercial keyword (e.g. "electric dirt bikes UK").
**Eligible secondaries:** brand name variations, top category umbrella terms (not deep long-tail modifiers — those belong on their own dedicated product/category pages, never stuffed onto the homepage). Do not run homepage secondaries through the Google-related-search / generated-transactional-modifier supplementation process used elsewhere — homepage secondaries should stay close to the primary, not padded out to a count.
**On-page notes:** Homepage is a hub — keywords should appear in hero headline, intro paragraph, section headings, and meta description. Do not force product-specific keywords onto the homepage.

### 4. Existing Blog Post
**Condition:** Cluster is informational/commercial AND a directly relevant blog post already exists
**Action:** Assign cluster to improve that post (add a content refresh flag)
**On-page notes:** Flag specific sections where keywords should be added or headings updated

### 5. New Product Page (Gap Flag)
**Condition:** Transactional cluster with no matching product on the site
**Action:** Flag as product gap → route to product-gaps.md
**Include:** Proposed URL slug, proposed page title, primary keyword, all cluster keywords

### 6. New Category Page (Gap Flag)
**Condition:** Commercial cluster for a product category the site doesn't have a page for
**Action:** Flag as category gap → route to product-gaps.md
**Include:** Proposed URL, proposed title, primary keyword, which existing products would belong here

### 7. New Blog Post
**Condition:** Informational or commercial cluster with no existing page match
**Action:** Route to blog planning → becomes a blog brief in blog-plan.md

**Anchor on Informational.** Blog posts carry both Informational (guides/pillars) and Commercial (comparisons/reviews) primaries, but the content calendar's backbone — and every pillar post specifically — should be built from Informational primaries per the Intent Classification tie-break rule. If the blog plan is Commercial-heavy and Informational-light, the site is under-serving top-of-funnel search demand and missing easy, less-contested ranking opportunities.

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
**Every mapped page — product, category, brand hub, blog post — gets a page-specific mini-FAQ (2–4 Q&As) where the cluster has question-intent keywords to draw on, not just the homepage and the dedicated FAQ page.** This is a real organic-traffic lever, not decoration: each FAQ answer is indexable content that can absorb a secondary or LSI keyword naturally, so a page with a mini-FAQ competes for more query variations than the same page without one. Full rules, sourcing, and the "where possible" scope (some thin clusters genuinely have no question-intent keywords to draw on — don't invent questions) are in `references/content-planning.md` § Page-Level FAQ.

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

Run all three levels as a final check before the keyword-map is delivered — supplementation (Google related searches, generated modifiers, Low-KD Rescue keywords) draws from shared pools across many clusters, which makes secondary- and FAQ-level collisions a real risk that URL-level checking alone won't catch.

### 1. URL-level (primary keywords)
- List all assigned URLs
- Flag any URL that has been assigned more than one cluster
- If two clusters land on the same URL: merge them immediately

### 2. Secondary-level (the new risk — check this explicitly)
- Build a running registry of every secondary keyword used across every mapped page as you go through Phase 4/5, not just at the end
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

```
| Cluster Name | Primary KW | Vol | KD | Tier | Intent | Assigned URL | Page Type | Status |
|-------------|-----------|-----|-----|------|--------|-------------|----------|--------|
| Youth electric dirt bikes | electric dirt bikes for kids | 1300 | 22 | T1 | Transactional | /electric-dirt-bikes/youth/ | Category | Existing |
| Sur-Ron Light Bee review | sur-ron light bee x review | 480 | 31 | T2 | Commercial | /blog/sur-ron-light-bee-review/ | Blog | New |
```
