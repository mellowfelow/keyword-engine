# AI / GEO / AEO Visibility Reference

## Why This Layer Exists

Search is no longer just Google. AI assistants (ChatGPT, Claude, Gemini, Perplexity) now answer product questions directly. Voice assistants pull from structured content. GEO (Generative Engine Optimisation) and AEO (Answer Engine Optimisation) ensure your content gets cited, recommended, and quoted by these systems.

This layer annotates every page and blog post with seven visibility signals. Apply it after Phase 5 mapping and Phase 6 blog planning are complete.

---

## Signal 1: FAQ Schema (FAQPage JSON-LD)

**What it does:** Tells Google and AI crawlers exactly which questions this page answers and what the answers are. Eligible for rich results in Google. Feeds AI knowledge graphs.

**When to apply:**
- Any page or blog post with 2+ question-intent keywords in its cluster
- All FAQ sections on product pages, category pages, and blog posts
- The dedicated FAQ page

**Rules:**
- Answers must be self-contained (make sense without surrounding context)
- Answers must be 40–65 words — short enough for AI to extract directly (content-planning.md's Answer Rules ceiling: homepage FAQ 40–55, FAQ page 50–65, never exceed 65 in any answer)
- Do not mark up "fake" FAQs — only questions that are genuinely in the keyword data
- One FAQPage schema block per page (combine all Q&As into one block)

**Output in keyword-map.md:** Add column "FAQ Schema" = Yes/No per page
**Output in blog-plan.md:** FAQ schema block specified in every brief
**Output in faq-bank.md:** Full JSON-LD blocks per theme section

---

## Signal 2: Speakable Schema

**What it does:** Flags specific content blocks as "speakable" — optimised for text-to-speech reading by voice assistants (Google Assistant, Alexa, Siri) and for AI assistant answer extraction.

**When to apply:**
- The single best FAQ answer on each product and category page
- The definition hook paragraph on blog posts
- The introduction paragraph of the homepage

**Rules:**
- Speakable content must be 1–3 sentences maximum
- Must read naturally when spoken aloud — no markdown, no bullet points
- Must be genuinely answering a question, not marketing copy
- Use WebForge's class-based CSS selector convention — never ID selectors. WebForge generates classes, not IDs, so ID selectors will not match anything at build time.

**WebForge class conventions for speakable targets:**
- Homepage brand statement: `.brand-statement`
- Homepage hero description: `.hero-description`
- About page intro: `.about-intro`
- Best FAQ answer per page: `.faq-answer-speakable`

**Output format per page:**
```
Speakable target: [CSS class — e.g. .faq-answer-speakable]
Content to mark up: "[The actual sentence(s)]"
WebForge instruction: Add class="faq-answer-speakable" to this element during build
```

---

## Signal 3: Entity Coverage

**What it does:** AI models and knowledge graphs understand content through named entities — brands, products, locations, people, specifications. Pages without clear entity mentions are harder for AI to categorise and cite.

**What to check per page:**

| Entity Type | Examples | Where It Should Appear |
|-------------|---------|----------------------|
| Product entity | "Sur-Ron Light Bee X", "48V electric dirt bike" | H1, first paragraph, product title |
| Brand entity | "Sur-Ron", "Talaria", "KTM" | H1 or H2, brand section, meta description |
| Category entity | "electric dirt bikes", "youth off-road bikes" | H1, intro, breadcrumb |
| Location entity | "US", "UK", city/region if relevant | Meta description, shipping info, footer |
| Spec entities | "1500W motor", "48V battery", "top speed 45mph" | Product specs section, structured data |

**Flagging rule:** If any of these entity types is missing from a page's cluster, flag it as "Entity Gap: [type]" in keyword-map.md.

**Fix:** The on-page brief for that page should include a note to explicitly name the missing entity in the copy.

---

## Signal 4: Featured Snippet Hooks

**What it does:** The "definition hook" — a 1–2 sentence plain-language answer positioned in the first 150 words of a page. Google extracts these for position-zero featured snippets. AI assistants extract these for direct answers.

**When to apply:**
- Every blog post (especially informational and commercial intent)
- Category pages (define what the category is at the top)
- FAQ page intro

**The formula:**
```
[Primary keyword capitalised] [are/is] [plain-language definition].
[1 supporting sentence with a secondary keyword].
```

**Examples:**
- "Electric dirt bikes for kids are battery-powered off-road motorcycles designed for riders aged 3–14. They offer a safe, quiet alternative to petrol bikes with adjustable speed limits and lightweight frames."
- "The Sur-Ron Light Bee X is a high-performance electric off-road bike with a 6kW mid-drive motor and 60V battery system, popular with riders aged 14 and up."

**Rules:**
- No marketing language ("amazing", "best-in-class") in the hook — AI models distrust promotional framing
- Must directly answer what the primary keyword implies
- Should stand alone as a complete answer with no additional context needed

**Output format in blog-plan.md:** Each brief includes a "Definition Hook Draft" field — a pre-written 1–2 sentence hook for the writer to place in the intro.

---

## Signal 5: llms.txt Priority Map

**What it does:** The `llms.txt` file tells AI crawlers which pages on your site are most authoritative and should be prioritised for inclusion in AI knowledge bases. It's the AI equivalent of a sitemap.

**Selection criteria for llms.txt inclusion:**

| Priority | Page Type | Reason |
|----------|-----------|--------|
| P1 — Always include | Homepage, main category pages, brand pages | Core authority pages |
| P1 — Always include | FAQ page | Directly feeds AI answer extraction |
| P2 — Include if Vol 500+ | Top product pages | High-demand individual products |
| P2 — Include if 1000+ words | Pillar blog posts | Topical authority signals |
| P3 — Optional | Standard blog posts | Include if they cover unique topics |
| Exclude | Tag pages, pagination, thank-you pages, account pages | Low value, noise |

**Output at end of session:**
```markdown
## llms.txt Priority Map

### P1 — Core Pages (always include)
- / — Homepage
- /electric-dirt-bikes/ — Main category
- /brands/ — Brand hub
- /faq/ — FAQ page

### P2 — High-Value Pages
- /electric-dirt-bikes/youth/ — Youth category (Vol: 3200 combined)
- /brands/sur-ron/ — Sur-Ron brand page (Vol: 2800 combined)
[...]

### P3 — Content Pages
- /blog/best-electric-dirt-bikes-for-kids/ — Pillar post
[...]

### Exclude
- /cart/, /account/, /tag/, /page/2/ [etc.]
```

This map feeds directly into the WebForge workflow for building the actual `llms.txt` file.

---

## Signal 6: SERP Feature Targeting

**What it does:** Not every query gets the same SERP treatment — some trigger a featured snippet, some a People Also Ask box, some an image pack, some a shopping/product pack. Building every page in the same generic format wastes the pages that could actually win a feature. This signal matches page structure to the feature the primary keyword's SERP is actually showing.

**When to apply:** Every mapped page and blog post, during Phase 5/6, before the on-page brief is finalised.

**How to check:** Use `web_fetch` on the live SERP for the primary keyword (same mechanism already used for related-search supplementation in Phase 4) and note what's showing above the organic results.

| SERP Feature Detected | Structural Response |
|------------------------|---------------------|
| Featured snippet (paragraph) | Place a 40–50 word direct-answer paragraph immediately under the H1, before any other content — this is the exact shape Google lifts into the snippet |
| Featured snippet (list) | Structure the relevant section as a numbered or bulleted list with a short lead-in sentence — ordered steps for "how to," ranked items for "best X" |
| Featured snippet (table) | Include a comparison/spec table with the queried data as its own rows — this is already required for "best/vs" posts under GEO Rule 2 (Comparison Readiness), so this just confirms when it's load-bearing, not optional |
| People Also Ask | Mine the PAA questions shown and fold the relevant ones into the page's page-level FAQ (Phase 7) — these are literally the questions Google has already confirmed real searchers ask next |
| Image pack | Make sure the page has at least one genuinely relevant, well-named, alt-texted image near the top — image packs reward pages Google can confidently attribute an image to |
| Shopping/product pack | Confirm Product schema (price, availability, review rating) is planned for this page — shopping packs pull directly from structured data, not prose |
| No visible feature (plain 10 blue links) | No structural change needed — standard on-page formula applies |

**Output in keyword-map.md:** Add a "SERP Feature" note per page (e.g. "Snippet — table" or "PAA — 3 questions folded into FAQ") so the brief tells the builder exactly which structural element is load-bearing, not just a generic instruction to "write good content."

**Don't over-fit:** SERPs change. This is a best-effort structural hint based on what's showing right now, not a guarantee — note it as a recommendation, not a hard requirement, if the check is inconclusive or the SERP looks unstable (mixed feature types, obviously personalised results).

---

## Signal 7: AI Overview / AI Assistant Citation Optimization

**What it does:** Signal 4 (Featured Snippet Hooks) already produces AI-extractable answers, but AI Overviews and chat assistants (ChatGPT, Perplexity, Claude, Gemini) have their own citation pattern that's narrower than a Google snippet — they favor short, self-contained, source-attributable statements over marketing prose, and they tend to cite pages that make verification easy.

**When to apply:** Every page and post that already has a Definition Hook (Signal 4) — this signal refines that hook's *format* specifically for AI-citation extraction, not a separate piece of content.

**The additional rules, on top of Signal 4's formula:**
- **Lead with the fact, not the brand.** "Electric dirt bikes for kids typically top out at 15–20mph" cites more easily than "At [Brand], our kids' bikes reach up to 20mph" — AI systems favor neutral, verifiable phrasing over promotional framing, and pages that read as objective get cited over pages that read as sales copy.
- **One claim per sentence.** AI extraction tends to pull single sentences, not whole paragraphs — a sentence that bundles two facts risks getting cited half-correctly or not at all.
- **Make the number/spec the anchor.** Where the answer includes a number (price, speed, weight, age range), put the number early in the sentence, not buried at the end.
- **Keep a plain-text-extractable version.** Don't put the load-bearing fact only inside an image, table caption, or JS-rendered widget — AI crawlers extract from rendered page text, not images or client-side-only content.
- **Consistency across pages is a citation trust signal, not just an accuracy nicety** — this is already covered under GEO Rule 1 (Cite-ability) below, but flag it here too: a page that states one spec and gets cited, only for the AI to find a contradicting number elsewhere on the site, damages future citation odds for the whole domain.

**Output in blog-plan.md / keyword-map.md:** No separate field — this is a formatting constraint applied to the existing "Definition Hook Draft" field from Signal 4. Note it as "AI-citation formatted" once the hook has been checked against the rules above.

---

## GEO (Generative Engine Optimisation) — Additional Rules

Beyond the seven signals above, apply these GEO principles across all content planning:

**1. Cite-ability**
AI models prefer content they can cite with confidence. Every factual claim on your site should be:
- Specific (numbers, specs, model names — not vague descriptions)
- Consistent across all pages (don't say "top speed 45mph" on one page and "up to 50mph" on another)
- Sourced where possible (manufacturer specs, official certifications)

**2. Comparison Readiness**
AI assistants frequently answer "what's the best X" by comparing options. Pages and posts that contain structured comparison tables (not just prose) are far more likely to be cited.
- Every "best of" or "vs" blog post must include a comparison table
- Category pages benefit from a "quick comparison" table of the top 3–4 products

**3. Freshness Signals**
Include a "Last updated: [month year]" note on:
- All blog posts
- Pillar guides
- Any page with pricing, availability, or spec information
AI models weight fresh content more heavily for product and price queries.

**4. Local Business Schema (situational — only sites with a physical location/service area)**
If the site has a physical location, showroom, or service area (see `references/filter-and-cluster.md` § Local Intent Layer), every location page gets `LocalBusiness` schema (not the generic `Organization` schema used elsewhere) with `address`, `geo`, `openingHours`, and `areaServed` fields populated. Multiple locations get one `LocalBusiness` block each, never one shared block covering all of them — same principle as not merging location clusters. Skip this entirely for a pure ship-anywhere ecommerce site with no physical presence.

**5. E-E-A-T Reinforcement**
Experience, Expertise, Authoritativeness, Trustworthiness — the signals Google and AI models use to assess content quality:
- About page with real business info
- Author bios on blog posts
- Physical address / contact info in footer
- Trust signals on product pages (warranty info, certifications, return policy)
Flag missing E-E-A-T elements when scanning the site in Phase 5.

---

## Quality Control — this file's own dedicated audit layer

Governed by Rule 5 (`core-rules.md`). Seven signals, a situational schema branch, and five GEO rules are too much distinct mechanics to leave to the general Mode A Quality Control alone.

**Pre-ship checklist (run before this layer's output ships, every session):**
1. **All seven signals were actually applied per mapped page, not just declared once at the session level** — a page with a planned FAQPage block but no Definition Hook (or vice versa) is a half-applied signal, not a pass.
2. **Entity Coverage's `knowsAbout[]` source was confirmed as homepage AND shop page together, not homepage alone** (Signal 3) — the one check in this layer most worth re-verifying, since it's the easiest one to get half-right.
3. **SERP Feature Targeting (Signal 6) ran per page, before that page's brief was finalized** — not skipped as "nice to have" or batched in afterward.
4. **Local Business Schema only applied where the site genuinely has a physical location/service area** (per `filter-and-cluster.md` § Local Intent Layer) — never defaulted on for a ship-anywhere site, and never one shared block covering multiple locations.
5. **Every Definition Hook (Signal 4) that's also AI-citation formatted (Signal 7) actually follows the additional rules** — fact-first, one claim per sentence, number anchored early, plain-text extractable — not just the base Signal 4 formula with the label added.
6. **No signal's output landed outside `keyword-map.md`/`blog-plan.md`/`faq-bank.md`** — this layer annotates the documents `niche-taxonomy.md` and Phase 5–8 already produce, it never creates a new output document of its own.

**Re-audit (later, same trigger pattern as every other Layer 2 in this skill):**
- Has a page's primary keyword changed since this layer last ran (a Reason-A/A2 promotion out of blog, a cannibalisation re-pick, a Mode B MISMATCH retarget)? Its FAQ Schema, Entity Coverage, and Definition Hook all key off the primary — re-run this layer for that page specifically.
- Has the live SERP's feature for a page's primary keyword changed (Signal 6)? SERPs drift — re-check periodically, not just at first build.
- Has `knowsAbout[]` drifted to homepage-only again after an edit to either the homepage or shop page's keyword set? Re-confirm both are still represented.
