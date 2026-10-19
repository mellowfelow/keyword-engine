# Phase 0 — Niche & Taxonomy Discovery

Runs **before** Phase 1 (Filter & Clean) when the user gives a keyword/niche
instead of a ready keyword list or product list. Produces a full, stockable
shop taxonomy from scratch. Feeds its category/subcategory output into
Phase 1–4 as seed clusters (see "Feeding into clustering" at the end of
this file) — not a disconnected side-output.

Governed by Rule 1 (`core-rules.md`): any source link/platform the user
names during this phase is used as given, no verification challenge.

**Step B's live platform research is governed by the same operational
rules as every other Semrush-driven phase** — `semrush-workflow.md`
(refresh-before-read discipline, the refresh quota with active tracking,
glitch/quota recovery via stop-notify-resume, the five-source harvesting
checklist). Those rules apply here in full; this isn't a separate, lighter
standard just because the research happens earlier in the pipeline.

---

## Trigger

Runs when the user supplies a **keyword or niche** (not a keyword list, not
an existing product list) and wants a shop built out from nothing. If a
product list already exists, skip Phase 0 — go straight to Phase 1 using
that list.

Required input before starting: **target market/location.** Always asked
upfront if not already given — never inferred from domain TLD or guessed.
No location, no research starts.

---

## Procedure

### Step A — Viability gate (runs first, hard stop on fail)

Confirms **demand + product reality** in the stated location. This checks
viability, not competition density — a thin competitor count is NOT a
failure condition here; it's a scaling input handled later in Step G, and
can legitimately mean a genuine underserved opportunity rather than a dead
niche. Conflating "few competitors" with "not viable" would wrongly kill
good niches, so the two are kept strictly separate.

Check via live web search:
- Is it sold by real retailers/marketplaces in that market right now? (even
  one or two confirmed real sellers is enough to confirm the category
  genuinely exists)
- Is demand trend flat/growing, not dead? (Google Trends or equivalent,
  scoped to the stated region)
- Is it a physical product category at all (not a service, not a
  non-product concept being mistaken for one)?

**Actual fail conditions (hard stop):**
- Not sold as a real product anywhere in the stated market
- Confirmed dead/declining trend
- It's a service or non-product concept, not a physical product category

**NOT a fail condition:** low competitor count alone. A thin competitor set
still passes Step A if genuine demand/product existence is confirmed. It
gets reflected later as a smaller tier (Step G) and an explicit
"underserved niche / opportunity" note in the output — never treated as a
reason to stop.

**Outcome handling — true fails only:**
- **Viable:** proceed to Step A2 (legal/compliance check), then Step B.
- **Fails one of the actual fail conditions above:** STOP. Do not build a
  taxonomy. Report clearly: what was checked, what was found, why it
  fails, and stop there. Do not auto-pivot to an adjacent niche and do not
  produce a "best effort" taxonomy anyway. The user must redirect
  explicitly (new niche, override, or confirm they want to proceed despite
  the finding) before anything continues.

### Step A2 — Legal/compliance flag

If the niche is age-restricted or regulated in the stated location
(alcohol, vape/nicotine, supplements, weapons/knives, cannabis-adjacent,
etc.), flag this explicitly as part of the viability report — before
building the taxonomy, not buried later. This is a flag/notice, not a
second hard stop; regulated niches are buildable (this skill has already
shipped them), the user just needs to see the flag to decide how to proceed.

**Distinction from Step A:** this step is for niches that are **restricted
but legally sellable** (age verification, licensing, etc.). A niche that is
flatly **illegal to sell** in the stated location shouldn't reach here at
all — it should already fail Step A's "sold by real retailers right now"
check, since no real sellers will be found. If A2 is reached, the niche has
already passed as a real, legally sellable (if regulated) category.

### Step B — Competitor scan

Identify a working set of real competitor stores selling in this niche, in
the stated market. Pull from each:
- Full nav menu (categories + subcategories as the competitor structures
  them)
- On-site filters (filters often reveal attribute-level subcategories that
  don't show in the main nav)
- Homepage/collection "best sellers," "trending," "most popular" sections
- Brand listings / brand filter sidebar
- **Their actual ranking keywords, where available** (Rule 4 — competitor
  keywords as a standing research input, not just structural scanning). If
  a competitor's Semrush Organic Research/Keyword Gap export is provided,
  pull it here too — it often surfaces sub-niches and product types that
  nav/filters alone miss, strengthening the taxonomy itself.
- **A rough price range per category/subcategory** — not a per-product
  price database, just a lightweight note of what competitors charge
  within each category as it's scanned anyway. `product-gaps.md`'s
  high-ticket determination reads this data later — capturing it here,
  once, while the competitor's page is already open, is far cheaper than
  reconstructing it later from memory in a separate session.

**Minimum source requirement:** at least 5 real competitor sources (more
for Large/Massive tiers), mixing source types — dedicated ecommerce stores
AND marketplaces (Amazon/eBay/Etsy/local equivalents) — so the result
isn't skewed by one retailer's idiosyncratic categorization. If genuine
effort can't surface 5+ sources (true for some thin/emerging niches), note
the shortfall explicitly in the output — this caps confidence (Step E/F),
not viability (Step A).

**Source quality requirements** (a source only counts toward the minimum
if both hold):
- **Independent:** a genuinely separate business — not the same
  retailer's regional mirror/duplicate domain counted twice.
- **Niche-scoped:** the data pulled must be specific to this niche, not
  whole-site aggregate data from an unrelated mega-retailer where the
  niche is one small corner of a huge, unrelated catalog. If the only
  "competitor" found is a department-style store, pull only its
  niche-relevant section, not its site-wide SKU count.

### Step C — Taxonomy skeleton

Use a standard ecommerce taxonomy backbone (Google Product Taxonomy /
Shopify standard product categories) as the structural skeleton, so output
shape is consistent across any niche run — not reinvented ad hoc each time.

### Step D — Niche-specific layer

Graft the real subcategories found in Step B onto the Step C skeleton.
Canonicalize naming across competitors before finalizing — different
stores label the same category differently (e.g. "Spirits" / "Hard
Liquor" / "Liquor"); the output tree uses one consistent label per node.

**Sequencing rule:** canonicalization happens here, before Step E/F. Brand
and product confidence counting (Step E/F) always runs against the
canonicalized tree, never the raw per-competitor labels — otherwise the
same real category could get wrongly split across its label variants and
show artificially low confidence.

### Step E — Top brands

Brands that recur across multiple competitors in this niche/market = "top
brands." List them per category/subcategory where relevant.

**Sourcing policy:** list all brands found, regardless of whether
dropship/wholesale access can be confirmed. No sourcing/stockability check
is performed — sourcing and dealership arrangements are entirely the
client's.

**Confidence tag:** every brand gets a High/Medium/Low tag based on how
many Step B sources agreed on it, counted against the canonicalized
category tree from Step D:

| Confidence | Criteria |
|---|---|
| High | Appeared in ≥60% of scanned sources, OR an explicit bestseller/trending badge on 2+ sources |
| Medium | Appeared in 2+ sources but below the 60% threshold |
| Low | Appeared in only 1 source, or inferred from a weak single signal |

### Step F — Top/most-popular products

Per category/subcategory, identify representative popular products using:
- Bestseller/"trending"/"most popular" badges or sections on competitor
  sites
- Repeated presence of the same product type across multiple competitors
- Review volume as a popularity proxy where visible

Same sourcing policy as Step E: list what the research surfaces, regardless
of stockability. No sales-data access exists, so this is popularity-by-
signal, not verified sales figures — note this once in the output, not as
a constant hedge throughout.

**Confidence tag:** same High/Medium/Low scale and criteria as Step E,
same canonicalized-tree basis, applied to products instead of brands.

**Filtering rule (applies to both E and F):** output includes High +
Medium by default. Low-confidence items are only included when needed to
meet the Step G tier's target count (reality-over-target rule still
applies — real findings first), and when included, they stay explicitly
marked Low — never silently blended in as if equally certain as a
High-confidence entry.

The fewer sources Step B found, the lower the confidence ceiling across the
whole output — thin research produces a taxonomy that's honest about being
thin, not one dressed up to look as certain as a well-sourced run.

### Step G — Depth/breadth scaling

Tree size and product-count-per-subcategory scale to two measured signals:
1. **Search volume tier** for the core niche/keyword, scoped to the stated
   location.
2. **Median competitor SKU count** observed in Step B (the real-world size
   of the category, as actually stocked by live competitors).

**Conflict rule:** if the two signals disagree (e.g. high search volume
but thin competitor catalogs — a "trendy search term, not a real built-out
market" case), use the **lower/smaller tier**. Never build a bigger
taxonomy than what competitors are actually stocking, regardless of search
hype.

**Tiers:**

| Tier | Monthly search volume (core term, scoped to location) | Competitor median SKUs | Categories | Subcategory depth | Products per subcategory |
|---|---|---|---|---|---|
| Micro | <500 | <50 | 3–5, flat | none | 5–10 total |
| Small | 500–5,000 | 50–200 | 4–8 | 1 level, optional | 10–20 |
| Medium | 5,000–20,000 | 200–1,000 | 6–12 | 1 level | 15–25 |
| Large | 20,000–100,000 | 1,000–5,000 | 10–20 | 2 levels | 20–35 |
| Massive | 100,000+ | 5,000+ | 15–30+ | 2 levels | 25–50 |

The final tree is also capped by actual market breadth — the number of
distinct sub-niches real competitors carry (Step B). The tier sets the
target size; Step B's findings set the ceiling on what subcategories can
legitimately exist.

**Reality-over-target rule:** the tier is a target, not a mandate. Never
invent a category, subcategory, or product to hit the tier's number. If
research only supports fewer categories than the tier suggests, output
what's real and say so plainly (e.g. "research supported 4 categories; the
Medium tier typically suggests 6–12"). If research surfaces more than the
tier's top end, fold the extras in as subcategories of existing categories
rather than sprawling the top level wider. Findings always override the
target.

### Step H — Output

Saved alongside Mode A's other strategy docs, in the project's `docs/`
folder — not a separate location.

Produces two files:

**`taxonomy-map.md`**
- Full category → subcategory tree (canonicalized)
- **Rough price range per category/subcategory** (from Step B) — the
  durable home for this data. `product-gaps.md` reads this later to
  determine whether a candidate product is "high-ticket" relative to the
  niche.
- Top brands per category/subcategory, each tagged High/Medium/Low
  confidence
- Top/popular products per category/subcategory, each tagged High/Medium/
  Low confidence (with the "popularity by signal, not verified sales" note
  stated once, up top)
- **Sources section** — a table of every competitor/source checked: name/
  URL, source type (dedicated store / marketplace), what was pulled from
  it (nav / filters / bestsellers / brands), and the date checked
- Viability verdict + any legal/compliance flag from Step A/A2
- **Underserved-niche note** when Step B found fewer than ~5 real
  competitors despite genuine effort — framed as a possible opportunity
  signal, not a defect in the research
- **Seasonality note** when the niche is seasonal: states whether research
  was done in-season or off-season, and that off-season research is normal
  when a client is building ahead of season to rank early
- **Location-scope note**: this taxonomy is valid for the one stated
  market only. Expansion into another market (common for EU multi-country
  clients) requires a separate Phase 0 run per additional market
- **Re-run recommendation**: niches drift; recommend re-running Phase 0
  (or the Taxonomy Re-Audit below) periodically rather than treating this
  as a permanent, one-time snapshot

**`starter-product-list.csv`**
- Flat, stockable list: category, subcategory, product name, brand,
  confidence tag
- The literal "client can hand this to a supplier and start stocking"
  output

---

## Generating the keyword paste Phase 1 needs (Phase 0 → Phase 1)

**Phase 0 answers "what should the site sell." Phase 1–4 answer "which
keywords should it target" — a different question that needs real
Volume/KD/CPC data, which `taxonomy-map.md` doesn't carry.** When Phase 0
ran because the user had no keyword list to begin with, there is no
keyword paste for Phase 1 to filter yet, so generate one before handing
off:

Using the Semrush/platform link (Rule 1 — already in use for Step B, per
`semrush-workflow.md`), run Keyword Magic Tool against the taxonomy's
core niche term and every category/subcategory name from `taxonomy-map.md`
(not the individual products — that level of granularity is Phase 1's job
once real keyword variants surface). Export the resulting Keyword/Volume/
KD/CPC/Intent rows the same way a user-provided export would arrive, and
hand that off as Phase 1's input. This is routine use of an already-
provided link for a new query, not a new data source — same refresh-
before-read and quota discipline as every other search in
`semrush-workflow.md` applies.

If no Semrush/platform link is available at all (neither for Step B nor
this step), say so plainly and ask the user for one before Phase 1 can
run — never invent keyword Volume/KD/CPC data to keep the pipeline moving.

---

## Feeding into clustering (Phase 0 → Phase 1–4)

**Every category/subcategory in `taxonomy-map.md` becomes a seed cluster
before Phase 4 clustering runs.** When Phase 4 clusters the raw keyword
export, each natural cluster is checked against the seed clusters first:

- **Topical match to an existing seed cluster** → the new cluster's
  keywords join (extend) that seed cluster rather than forming an
  independent one. This is what keeps a category page's keyword set
  coherent with the taxonomy it's supposed to represent, instead of
  clustering purely from keyword text and only reconciling against the
  taxonomy afterward.
- **No match to any seed cluster** → ordinary independent clustering
  (Phase 4's normal process) applies. If the resulting cluster is strong
  enough to need its own page but has no home in the taxonomy, it surfaces
  as a normal Category Gap (`page-mapping.md`'s New Category Page flag) —
  no separate mechanism needed, the taxonomy just didn't anticipate it.

This is the one connection point between taxonomy research and keyword
clustering — everything else about Phase 1–4 (filtering, intent, scoring)
runs exactly as it does without Phase 0.

---

## Quality Control — this file's own dedicated audit layer

Two layers, governed by Rule 5 (`core-rules.md`) — the general, skill-wide
orchestration layer sitting on top of this phase's own checklist. Rule 5
doesn't restate anything checked below — it defines what happens when a
line here fails: that failure sends Phase 0 back for rework and a re-run
of this exact checklist until it's genuinely clean or the failure is a
validated Honest Shortfall per Rule 5's own test.

### Pre-ship self-audit (runs every time, before output ships)

Immediately after Step H, before `taxonomy-map.md` and
`starter-product-list.csv` are handed to the user, run through this
checklist in full. Any failure gets fixed before output ships, not
disclosed as a known issue and shipped anyway.

**Step A / A2 — Viability & compliance**
- [ ] Step A ran, and if it failed on an actual fail condition (not just
      low competitor count), the hard stop happened — no taxonomy was built
- [ ] **The stop itself reported correctly, not just occurred** — what was
      checked, what was found, and why it fails are all stated; no
      auto-pivot to an adjacent niche happened; no "best effort" taxonomy
      was produced anyway; the user was left to redirect explicitly
- [ ] Location was confirmed before research started, not assumed/inferred
- [ ] Legal/compliance flag checked and, if applicable, surfaced near the
      top of the output as part of the viability report — not checked-
      but-buried later, and not escalated into a second hard stop

**Step B — Competitor scan**
- [ ] Met the 5-source minimum scaled to tier — 5+ for Micro/Small/Medium,
      more for Large/Massive. If genuinely short, the shortfall is
      explicitly noted AND the confidence ceiling was actually capped as
      a result — not noted as a caveat while the rest proceeds at full
      confidence anyway
- [ ] Source mix includes more than one source type
- [ ] Every counted source is independent (no duplicate/mirror domains)
- [ ] Every counted source is niche-scoped (no whole-site aggregate data
      from an unrelated mega-retailer)
- [ ] Competitor ranking-keyword data was pulled where available (Rule 4),
      not just the structural nav/filter/bestseller/brand scan
- [ ] A rough price range per category/subcategory was actually captured
      while scanning each source, not left as an unrecorded impression
- [ ] Every keyword/competitor data point was refreshed/updated before
      being read or recorded (`semrush-workflow.md`'s rule, applied here
      in full, not a lighter standard for this earlier phase)
- [ ] Refresh quota was tracked actively across this session; any glitch
      or quota exhaustion was met with stop-notify-resume, never a restart
      from scratch

**Step C — Taxonomy skeleton**
- [ ] A standard taxonomy backbone was actually used, not an ad hoc tree
      invented from scratch

**Step D — Canonicalization**
- [ ] Category/subcategory naming was canonicalized across competitors
- [ ] Canonicalization happened *before* Step E/F confidence counting

**Step E / F — Brands, products, confidence**
- [ ] No stockability filtering was applied — everything found is listed
- [ ] Every brand/product in the output carries a confidence tag
- [ ] Each tag was actually computed against the stated thresholds — not
      loosely estimated
- [ ] High and Medium confidence items are included by default
- [ ] No Low-confidence item is blended in silently — only present when
      needed to hit a tier target, and still marked Low
- [ ] The popularity-by-signal disclaimer is present exactly once, up top

**Step G — Scaling**
- [ ] When volume tier and competitor-SKU tier disagreed, the lower tier
      was used
- [ ] Category, subcategory, AND product-per-subcategory counts all match
      what Step B's findings actually support — no invented items to hit
      the tier number
- [ ] Tree does not exceed the number of distinct sub-niches Step B
      actually found

**Step H — Output**
- [ ] Sources section includes all four required fields per source
- [ ] The rough price range per category/subcategory is actually written
      into `taxonomy-map.md`
- [ ] The viability verdict itself is written into `taxonomy-map.md`
- [ ] Underserved-niche note included if applicable
- [ ] Seasonality note included if the niche is seasonal
- [ ] Location-scope note included
- [ ] Re-run recommendation included
- [ ] Both files saved to the project's `docs/` folder
- [ ] `starter-product-list.csv` includes all five required columns

**Feeding into clustering**
- [ ] Every category/subcategory in the taxonomy was actually seeded as a
      cluster anchor before Phase 4 ran — not left for Phase 4 to
      discover independently and reconcile afterward

### Taxonomy Re-Audit (later, user-triggered, like Mode B)

Re-validates a previously generated `taxonomy-map.md` against the live
market, the same way Mode B re-validates keyword state against a live
site. Re-runs the relevant parts of the pre-ship checklist against fresh
data, not just a handful of drift questions:

- Is the original viability verdict still accurate? (Step A re-run)
- Is the legal/compliance status unchanged? (regulations can shift)
- Have the top brands/products changed since the original research? (Step
  E/F re-run, with fresh confidence tags — old tags are not carried over
  as-is)
- Has the competitor set shifted (new entrants, closures)? Re-check that
  the current source set still meets the independence + niche-scoping
  requirements, not just that sources exist
- Has the tier changed? (volume or median competitor SKU count may have
  moved the niche into a different Step G tier — resize the tree to
  match, following the same reality-over-target rule as a fresh run)
- Has the competitor set's own ranking-keyword profile moved since the
  original pull (Rule 4)? Re-pull Organic Research/Keyword Gap data rather
  than treating the first enrichment pass as permanent.
- Has the recorded price range per category gone stale? Re-check it,
  since `product-gaps.md` reads this range directly for any still-pending
  Gap candidates.
- Flags drift and updates `taxonomy-map.md` / `starter-product-list.csv`
  to match current reality, rather than leaving a stale snapshot in place.

**Closing gate:** once the re-audit updates the files, the full pre-ship
checklist runs again against the updated output before it re-ships. A
re-audited taxonomy is held to the exact same bar as a freshly generated
one.
