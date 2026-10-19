# Product Gap Analysis Reference

## What Counts as a Gap

A product gap exists when:
1. **Transactional keyword cluster** exists but no product/category/brand page on the site matches it
2. **Brand-navigational keywords** appear in the data but that brand has no page on the site
3. **High-volume commercial cluster** (e.g. "best 48V electric dirt bikes") has no corresponding category to send readers to
4. **Accessory keyword clusters** appear with no corresponding accessory pages or products

Gaps are separated into five types — Accessory is its own peer type, not a sub-case of Product Gap, matching how `output-formats.md`'s template counts and sections it separately:

### Brand Gap
Keywords: brand name + product type, brand name + model number, brand name + "review"
Signal: People are searching for a specific brand you don't stock or don't have a page for
Action: Stock the brand OR create a brand comparison page if stocking isn't viable

### Product Gap
Keywords: specific product type + transactional intent, specific model, specific spec (e.g. "48V 1500W electric dirt bike")
Signal: A product type or specification tier is being searched but you have nothing to sell them
Action: Source and stock the product type; propose URL and page structure

### Category Gap
Keywords: category-level term + commercial/transactional intent, "best [category]", "[category] for sale"
Signal: A whole product category exists in search demand but has no organisational home on your site
Action: Create the category page; identify which existing products belong there

### Accessory Gap
Keywords: "[product type] [part/accessory]", "[product type] upgrade", "[product type] replacement [part]", "[product type] kit" — see § Accessory Gap Detection below for the full pattern list
Signal: An accessory/part/bundle a buyer of the core product would reasonably want has no matching page or product on the site
Action: Source and stock the accessory; propose URL and page structure, grouped by accessory type

### Competitor Gap
Keywords: any query where a named competitor visibly ranks and this site doesn't have a comparable page
Signal: **Requires a competitor SEMrush export** (Organic Research or Keyword Gap report, exported the same way the site's own keyword data is — this skill has no SEMrush API access, competitor data arrives as a manual export same as everything else). If no competitor export is provided, skip Competitor Gap detection entirely rather than guessing from the primary keyword export alone.
Action: See § Competitor Gap Analysis below for the full workflow.

---

## Competitor Gap Analysis (Requires Competitor SEMrush Export)

**Input:** a competitor's SEMrush Organic Research export (or Keyword Gap report if the user ran one), same CSV/paste format as the site's own keyword export — Keyword/Volume/KD/CPC/Position columns.

**Skip cleanly if not provided.** This is an optional enrichment layer, not a blocker — Phases 1–8 run in full regardless. Only run this section when a competitor export is actually pasted in.

**This export does double duty.** Beyond gap detection below, the same competitor data is also a real-data source for Secondary Keyword Supplementation (`references/filter-and-cluster.md` § Secondary Keyword Supplementation) — a competitor's ranking keywords on a topic this site already has a page for become real, scored (`[competitor]`-tagged) secondary candidates, ranked above Google related searches since they carry actual Volume/KD/CPC rather than no data at all.

### Step 1 — Filter to genuine gaps
Cross-reference the competitor's ranking keywords against:
1. This site's own Primary Pool (Phase 1) — if the site already targets it, it's not a gap
2. This site's existing page inventory (Phase 5 site scan) — if a page already reasonably covers the topic even without the exact keyword, it's not a gap

What's left is keywords the competitor visibly ranks for that this site has no real coverage for at all.

### Step 2 — Run gap keywords through the same filters as any other keyword
Competitor-sourced keywords are not exempt from Phase 1's volume floor or Phase 3's KD ceiling — a competitor ranking for a KD 70 keyword doesn't mean this site should chase it. Apply the same intent-sensitive volume floor and KD tiers before treating anything as a real opportunity.

### Step 3 — Classify and route
- **Competitor is outranking on a keyword this site is close to targeting anyway** → strengthen the relevant existing/planned page's secondary keyword list
- **Competitor has a whole page type this site lacks** (a buying guide, a comparison hub, a specific product line, an accessory range) → route through Brand/Product/Category/Accessory Gap as normal, tagged with which competitor's coverage prompted it
- **Competitor's advantage is a brand/model this site genuinely doesn't stock** → Brand Gap, same as any other brand gap, but note the competitive pressure in the proposal's Opportunity section

### Output
```markdown
## Competitor Gap: [Gap Name]

**Competitor:** [competitor domain]
**Competitor's Ranking Keyword(s):** [keyword] (Vol: X, KD: X, competitor position: X)
**This Site's Current Coverage:** None / Partial — [why it's a real gap]
**Routes To:** Brand Gap / Product Gap / Category Gap / Accessory Gap / Existing Page Strengthening — [which, and why]

[If routing to a new gap proposal, use the Full Proposal Template above and tag it "Competitor Gap" in the Gap Type field]
```

Add a **Competitor Gap Summary** table at the top of product-gaps.md when this section runs:
| Competitor | Gap Keyword | Vol | KD | Routed To | Priority |
|-----------|-------------|-----|-----|-----------|----------|
| [domain] | [keyword] | [v] | [k] | [gap name / page] | T1/T2 |

---

## Link Magnet Candidates

**Why this exists:** every other section of this skill optimizes existing/planned pages to rank. This section flags content worth building specifically to *earn links and organic shares* — the on-page lever for attracting backlinks and referral traffic, not just search traffic. Run this once per session, after Phases 1–8, using the full keyword/cluster/catalog picture already built.

**Flag 1–2 realistic candidates per session — quality over volume.** A single genuinely link-worthy asset outperforms a list of generic ideas nobody will actually build. Don't force a candidate if the niche doesn't obviously support one; say so instead of padding the list.

### What to look for
Scan the clusters, product catalog, and Competitor Brands list (Phase 1) for genuine link-magnet angles:

| Type | What Makes It Link-Worthy | Signal to Look For |
|------|---------------------------|---------------------|
| **Free tool/calculator** | Solves a real decision problem (sizing, cost, compatibility) — gets linked to because it's useful, not because it's asked for | Repeated "which/how do I choose/how much" query patterns across clusters |
| **Original data/survey** | Citable by journalists and bloggers who need a source, not an opinion | Niche has an obvious "we surveyed/tested X" angle the site could genuinely run |
| **Comprehensive resource hub** | Becomes the canonical reference other sites link to instead of writing their own version | A pillar topic (Phase 6) broad enough to be the definitive guide, not just another article |
| **Comparison/VS content** | Naturally attracts links from forums, review sites, and affiliates citing "which is better" | Competitor Brands list (Phase 1) has 2+ genuine head-to-head comparisons worth making |
| **Downloadable resource** | Buying guides, size charts, checklists — low effort, decent link bait, can be gated for email capture | A cluster with strong "buying guide"/"checklist" informational intent |
| **Embeddable widget/badge** | Sites that embed it link back by design (e.g. a size-chart widget, a "verified dealer" badge for resellers) | Site has a B2B/reseller/affiliate angle where other sites would want to display something |
| **Digital PR hook** | A genuinely newsworthy or seasonal angle pitchable to journalists/bloggers, not standard SEO copy | A trend, seasonal spike, or original data point identified during clustering |

### Output
```markdown
## 🔗 Link Magnet Candidates

### Candidate 1: [Name/concept]
**Type:** Free tool / Original data / Resource hub / Comparison / Downloadable / Widget / Digital PR
**Why it's link-worthy:** [1–2 sentences — what makes this genuinely worth linking to, not just SEO-adjacent]
**Signal it's based on:** [which cluster(s)/catalog pattern/competitor gap prompted this]
**Suggested format:** [tool spec / data collection method / hub structure / comparison scope]
**Target keywords it also supports:** [tie back to existing clusters where relevant — this should double as an SEO page, not just a link bait exercise]

[Repeat for Candidate 2 if a genuine second one exists — otherwise state "one strong candidate this session; a second wasn't forced"]
```

If no realistic candidate exists this session, state plainly: "No strong link-magnet candidate identified this session — [brief reason, e.g. niche too narrow, catalog doesn't support an original-data angle]." Never manufacture a weak candidate just to fill the section.

---

## Demand Signal Calculation

For each gap, calculate a Demand Signal score:

```
Demand Signal = Sum of all keyword volumes in the gap cluster
```

Rank gaps by Demand Signal descending. Highest demand = highest priority to stock/build.

Also flag:
- **CPC signal:** If CPC is high (>£2 / >$2.50), it means competitors are paying to appear for this — strong buying intent
- **Trend signal:** If multiple related gap clusters all point to the same product type, it's a category-level opportunity not just a single product

---

## Full Proposal Template

For every gap identified, output:

```markdown
## [Gap Type]: [Gap Name]

**Gap Type:** Brand Gap / Product Gap / Category Gap / Accessory Gap / Competitor Gap
**Priority:** T1 / T2 (based on primary keyword tier)
**Demand Signal:** [combined volume of all cluster keywords]
**CPC Signal:** [average CPC across cluster — high/medium/low]

---

### The Opportunity
[2–3 sentences explaining what people are searching for and why this gap matters]

### Suggested Products/Brands to Stock
| Item | Why | Est. Demand Signal |
|------|-----|-------------------|
| [Product/Brand name] | [Reason: keyword volume, buyer intent, gap in your range] | [volume] |
| [Product/Brand name] | [Reason] | [volume] |

### Suggested Page Structure
- **URL:** /[proposed-slug]/
- **Page Type:** Product page / Category page / Brand page
- **Page Title:** [Suggested title including primary keyword]
- **H1:** [Suggested H1]
- **Primary Keyword:** [keyword] (Opportunity Score: X, Vol: X, KD: X, Tier: T1/T2)
- **Secondary Keywords (5+ minimum, fully assembled — same rule as any mapped page):** [kw1], [kw2], [kw3], [kw4], [kw5] [related-search], [kw6] [generated] — run every gap proposal through Secondary Keyword Selection Rules + Supplementation (filter-and-cluster.md) BEFORE it goes in this document, exactly as if it were already a live page. **The whole point is that when the client says "build this," the keyword package is already complete — no extra research step, no delay between the decision and the build.**
- **Content Notes:** [What should be on this page — specs, brand info, product range, etc.]
- **Page-Level FAQ candidates:** [2–4 Q&As if the cluster has question-intent keywords or an obvious buyer question — see content-planning.md § Page-Level FAQ. Pre-drafted here for the same reason as the secondaries: ready to build on decision, not after.]

### Internal Link Plan
- This page should link TO: [relevant categories, accessories, blog posts]
- These pages should link TO this: [existing pages that should reference it]

### Revenue Potential Notes
[Brief note on why this gap is worth filling from a sales perspective]
```

---

## Accessory Gap Detection

Look for keyword patterns like:
- "[product type] [part/accessory]" — e.g. "electric dirt bike battery", "electric dirt bike charger", "dirt bike helmet for kids"
- "[product type] upgrade" — signals aftermarket accessory demand
- "[product type] replacement [part]" — spare parts demand
- "[product type] kit" — bundle opportunity

These become accessory product gap proposals, grouped by accessory type.

---

## Competitor Brand Handling

When a competitor's brand name appears in the keyword data (from the Competitor Brands list built in Phase 1):

**Option 1 — Comparison content (recommended)**
Create a comparison blog post: "[Competitor Brand] vs [Your Brand/Alternative]"
→ Routes to blog-plan.md as a commercial cluster

**Option 2 — Alternative page**
Create a "[Competitor Brand] alternatives" page if search volume is high enough
→ This is a commercial landing page, not a product page

**Never:**
- Use a competitor brand name as the primary keyword on a product page
- Claim to sell a product you don't carry
- Create pages that are deceptive about brand affiliation
