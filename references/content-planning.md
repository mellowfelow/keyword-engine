# Content Planning Reference

## Blog Planning Rules

### Who Gets a Blog Post
Every cluster mapped to "new blog post" (page-mapping.md §7) gets a full brief, under the Reason A/B split that governs which clusters are even blog-eligible:
- **Reason A — true orphan, too low volume.** A Transactional keyword that never clustered with anything, vol 20–99, and isn't already claimed by a real taxonomy category, the homepage/shop, FAQ, an active conditional page, a stocked product, or a stocked brand → blog post.
- **Reason B — real volume, no matching product/category** → never blog; routes to a Gap Flag instead (product-gaps.md).
- Any Commercial cluster (vol ≥20) that didn't map to a product/category page → blog post.
- Any comparison keyword cluster → blog post, **unless the site has an active Compare page** (page-mapping.md's conditional page types) — a static Compare page and a Commercial "X vs Y" blog post must never target the same pair; if both could cover it, Opportunity Score decides which keeps it, and the comparison cluster never goes to a product page either way.
- Maximise the number of posts: if a cluster is viable under Reason A or Commercial, write the brief — Informational is sourced last, as filler once Reason-A/Commercial are exhausted, never ahead of them.

### ⭐ Launch Batch Floor — Tiered by Niche Size, Plus a Growing Backlog Toward 1000+

**Every session must deliver a complete launch batch, ready to build immediately, sized to the niche's breadth — not a flat number:**

| Niche tier | Rough sizing proxy (catalog/category breadth) | Launch batch (ready at go-live) |
|---|---|---|
| Micro/Small | Single narrow niche, <50 products or 1–3 categories | 25–30 |
| Medium | Moderate breadth, ~50–300 products or 4–10 categories | ~40–60 |
| Large | Broad catalog, ~300–1000 products or 10+ categories | ~70–100 |
| Massive | Very broad/multi-category, 1000+ products | 100+ |

This sizing proxy is a lightweight stand-in — a fuller niche/taxonomy classification (confidence tags, category depth, full taxonomy mapping) is a separate, more detailed research pass not yet folded into this skill's main numbering. Use judgment on which tier a niche falls into; the table above is enough to size the launch batch correctly in the meantime.

All briefs written and in blog-plan.md before the session ends — not trickled out over the 12-week calendar. Beyond the launch batch, keep planning: queue every additional viable topic as a backlog entry in blog-plan.md itself (see Content Calendar below), toward the 1000+ overall target where the niche supports it. The tier's number is a minimum, not a target.

**Sourcing order, strict:** Reason-A Transactional (vol 20–99) → Commercial (vol ≥20) → Informational, only once T+C are exhausted. This replaces the old blanket "maximise posts" framing with the same sourcing discipline as every other page type in this revamp.

**If the natural clusters don't reach the tier's launch batch target**, expand the topic pool using the same principle as Secondary Keyword Supplementation (filter-and-cluster.md) — real data first, generated topics only to fill the gap, and T/C before Informational within the expansion too:

1. **Broaden Transactional/Commercial coverage first — Reason-A orphans and Commercial comparison/review angles, not Informational.** Re-scan for Transactional keywords (vol 20–99) that never clustered tightly enough to earn their own page, and Commercial keywords (vol ≥20) that didn't map to a product/category page — these make good standalone posts even as a smaller (2–4 keyword) cluster, and come before Informational in the sourcing order.
2. **Site-search query mining, if a site-search export was provided.** Real first-party queries (not just product searches) are direct evidence of what visitors want to read — mine the same export used for secondary supplementation (filter-and-cluster.md) for topic angles, not just keywords.
3. **Competitor content gaps, if a competitor SEMrush export was provided.** Any Transactional/Commercial keyword the competitor ranks for that this site has no blog coverage of at all is a real, evidenced topic — cross-reference against the Competitor Gap Analysis output (product-gaps.md) rather than re-deriving it separately.
4. **Derive topics from the product catalog.** Every product category reasonably supports a "how to choose," "how to maintain," "buying guide," and "FAQ roundup" post even without a matching keyword in the export — these are genuine, useful topics inferred from what the site sells, not invented filler. Label them clearly as catalog-derived rather than export-backed.
5. **Google related searches, applied to topics not just keywords.** Pull related-search and "people also ask" data for the site's core product/category terms and mine it for blog-worthy angles the original export didn't surface.
6. **Comparison and accessory angles.** Every competitor brand found via competitor keyword research supports a comparison post; every accessory/part pattern (product-gaps.md § Accessory Gap Detection) supports a "do I need X" or "how to choose X" post.
7. **Only once 1–6 above are exhausted, broaden Informational coverage** — question-intent and general-education keywords that didn't cluster tightly — as the last-resort fill, never ahead of the Transactional/Commercial expansion above.

**Never pad with genuinely content-less topics just to hit the tier's launch batch target.** If the niche is so narrow that even catalog-derived and comparison angles can't reach it, ship what's real and say so plainly in the session summary — e.g. "17 fully-briefed posts delivered against a 25-post Small-tier target; niche breadth doesn't support more without content-less padding" — rather than inventing a post with nothing to say. This is the same honesty principle as the secondary-keyword floor: a stated shortfall with a reason beats a silently padded number.

### Word Count by Cluster Size
| Keywords in Cluster | Content Type | Word Count |
|--------------------|-------------|-----------|
| 2–4 keywords | Focused article | 800–1200 words |
| 5–8 keywords | Standard article | 1200–2000 words |
| 9–12 keywords | Comprehensive guide | 2000–3000 words |
| 13+ keywords | Pillar content | 3000–5000 words |

### Pillar Identification
Scan all blog clusters. The top 3–5 by combined cluster keyword volume become pillar posts.
Pillars get:
- 3000–5000 words
- Their own internal link hub (all related cluster posts link back to this pillar)
- A "What's in this guide" contents section at the top
- Schema type: Article with HowTo or FAQPage nested

### Content Type Selection
| Cluster Signals | Content Type | Structure |
|----------------|-------------|---------|
| "best", "top", "recommended" | Listicle / Roundup | H2 per item, pros/cons, verdict |
| "vs", "compare", "difference" | Comparison | Side-by-side table, verdict |
| "how to", "guide", "tutorial" | How-To Guide | Numbered steps, tips, warnings |
| "review", "worth it", "honest" | Review | Specs, pros/cons, verdict, rating |
| "what is", "explained", "beginner" | Explainer | Definition, context, examples |
| Mixed informational | General Guide | H2 sections by subtopic |
| "how to maintain/use/care for", accessory/upsell | Care & Maintenance Guide | Steps/tips, accessory cross-links, no sales push — Loyalty-stage, sourced last |

### Funnel Position
- **Bottom of funnel (buy now):** Reason-A Transactional orphans (vol 20–99), comparison posts, reviews, "best X for [buyer type]" → publish first
- **Middle of funnel (considering):** Buyer's guides, "how to choose X", feature explainers → publish second
- **Top of funnel (awareness):** General educational content, "what is X" → publish last
- **Loyalty / post-purchase (a fourth category, additive — not a separate quota):** Care guides, accessory/upsell topics, "how to use/maintain X" → sourced only once Bottom/Middle/Top are satisfied, per the strict T→C→I order; sequences into the backlog rather than a dedicated week block, and counts toward the same batch/1000+ target as everything else.

---

## Full Blog Brief Template

For every blog post, output this complete brief:

```markdown
## Blog Brief: [Post Title]

**URL Slug:** /blog/[slug]/
**Status:** Pending / Built — flipped to Built once WebForge actually publishes this post; this is the field WebForge reads to find the next post to build (next unused = next Pending brief in priority order), replacing the old separate keyword-cluster.txt queue
**Funnel Position:** Bottom / Middle / Top / Loyalty (post-purchase — additive, sourced last, not a separate quota)
**Priority Tier:** T1 / T2
**Content Type:** Listicle / Comparison / How-To / Review / Explainer / Guide / Care & Maintenance Guide
**Target Word Count:** [number]
**Schema Type:** Article / HowTo / FAQPage / Review

---

### Keywords
- **Primary:** [keyword] (Vol: X, KD: X)
- **Secondary:** [kw1], [kw2], [kw3], [kw4], [kw5]
- **LSI/Supporting:** [list — secondaries default to KD ≤28, extending to the 29–35 fallback band only if genuinely needed to hit the minimum; nothing above 35 is ever used]

---

### Title & Meta
- **H1:** [Full title — keyword first]
- **Meta Description:** [145–160 chars, CTA included]
- **Title Tag:** [Max 60 chars]

---

### Content Outline
**Intro (150–200 words)**
- Open with the reader's problem/question
- Include primary keyword in first 100 words
- Definition hook: 1–2 sentence plain-language answer to the main query (featured snippet target)
- Preview what the post covers

**[H2: Section 1]**
[Brief description of what this section covers — 2 sentences]
  - [H3 if needed]
  - [H3 if needed]

**[H2: Section 2]**
[Brief description]

**[H2: Section 3]**
[Brief description]

[Continue for all major sections...]

**[H2: FAQ Section]**
[3–5 questions from the FAQ bank relevant to this post]

**Conclusion / CTA (100–150 words)**
- Summarise key takeaway
- Clear next step: link to product page / category / related post
- CTA text suggestion

---

### Internal Links
**This post should link TO:**
- [URL] — [anchor text suggestion]
- [URL] — [anchor text suggestion]
- [URL] — [anchor text suggestion]

**Pages that should link TO this post:**
- [URL] — [context: where on the page, what anchor text]
- [URL] — [context]

---

### Images
- **Image 1:** [Type: product/lifestyle/diagram] — [description] — Alt: "[alt text]"
- **Image 2:** [Type] — [description] — Alt: "[alt text]"
- **Image 3:** [Type] — [description] — Alt: "[alt text]"
[Add more as appropriate for word count]

---

### FAQ Section (for this post)
Include at bottom of post with FAQPage schema:

**Q: [Question]**
A: [40–65 word answer. Concrete. No "it depends." Direct answer in first sentence.]

**Q: [Question]**
A: [40–65 word answer]

**Q: [Question]**
A: [40–65 word answer]

---

### Schema Block
[Specify the JSON-LD schema type and key fields to include]
```

---

## Content Calendar Template

**The 12-week calendar is the visible planning window, not a cap on total output.** With a launch batch sized to the niche's tier (25–30 Micro/Small, up to 100+ Massive — see Blog Planning Rules above) and a 1000+ overall target where the niche supports it, the full backlog routinely extends well past week 12 — everything beyond the 12-week window still gets a full brief and is sequenced right in `blog-plan.md` with its own `Pending`/`Built` Status, for WebForge to pull once the first 12 weeks are built. There is no separate queue file. Sequence into the calendar:

```markdown
## 12-Week Content Calendar (first window — backlog continues beyond week 12 in this same document)

### Priority Logic
Week 1–4: All T1 Bottom-of-funnel posts (direct sales drivers)
Week 5–8: T1 Middle-of-funnel + T2 Bottom-of-funnel
Week 9–12: T2 Middle-of-funnel + T1/T2 Top-of-funnel
Beyond Week 12: remaining backlog, sequenced the same way (Bottom → Middle → Top, T1 before T2), with Loyalty/post-purchase content filled in last once Bottom/Middle/Top are satisfied — full list in the Backlog section below, not repeated here

---

| Week | Post Title | Primary Keyword | Type | Funnel | Tier | Word Count | Status |
|------|-----------|----------------|------|--------|------|-----------|--------|
| 1 | [title] | [keyword] | [type] | Bottom | T1 | [words] | Pending |
| 2 | [title] | [keyword] | [type] | Bottom | T1 | [words] | Pending |
...

---

### Pillar Posts (produce in parallel, publish in Week 4, 8, 12)
These are long-form anchors — start writing them week 1, publish later so cluster posts are already live and can link to them.

---

### Backlog Beyond Week 12
**Total briefed:** [n] posts ([n] scheduled in the 12-week window, [n] queued beyond it toward the 1000+ target)
All [n] backlog posts have complete briefs in this same document, each with its own `Pending`/`Built` Status — not held back for a future session, and not in a separate file.
```

---

## FAQ Rules

### FAQ Bank Structure
All question-intent keywords + question signals across all clusters feed here.

**Sources for FAQ questions:**
1. Keywords with question-format phrasing (does, can I, how long, will, should, is it)
2. Informational keywords that imply a question (e.g. "electric dirt bike age limit" → "What age can a child ride an electric dirt bike?")
3. Commercial keywords with doubt signals (e.g. "electric dirt bike worth it" → "Are electric dirt bikes worth the money?")

**Prioritization — where the platform's AI Visibility tool is available:** spend answer-first formatting effort first on questions whose keywords actually show AI-Overview/AI-chatbot presence right now, not uniformly across every question found. This doesn't change which questions get included (all three sources above still feed the bank) — it changes which ones get the most careful answer-first polish first when time is limited.

### FAQ Homepage (6–8 questions)
Selection criteria:
- Buying-related questions first (price, shipping, age, safety, returns)
- Questions that remove purchase objections
- Questions actual customers ask before buying
- Keep answers 40–55 words — short, punchy, confidence-building
- Every answer ends with a soft internal link or CTA

### FAQ Page (full bank)
Organisation:
- Group by theme (e.g. "About Our Products", "Ordering & Shipping", "Safety & Age", "Maintenance", "Brands")
- Each theme = one H2 section
- Questions = H3s within each section
- Answers: 50–65 words, include 1–2 keywords naturally, include one internal link

### Page-Level FAQ (product / category / individual brand / Brand Hub / shop / blog / active Sale / Best Sellers / New Arrivals / Compare / Wholesale — every mapped page, not just homepage + FAQ page)

**The goal is organic keyword coverage.** A page-level mini-FAQ is indexable content unique to that page — it lets a product or category page compete for question-style long-tail queries it otherwise has zero shot at, without diluting the page's primary keyword focus the way stuffing more prose would. This is the single easiest way to widen organic traffic per page without adding new pages.

**When to add one:** whenever the mapped cluster (primary + secondaries + LSI) contains **2 or more question-intent keywords**, or the page-mapping process surfaced obvious buyer questions for that specific product/category/brand even without a literal question-format keyword in the data (e.g. a youth electric bike product page almost always needs an age/safety question even if "what age" wasn't in the export — use judgment, same as the niche-relevance rule).

**When to skip it:** a thin cluster with no question-intent signal and no obvious buyer question for that specific page. Don't invent a question just to check a box — an empty or filler FAQ is worse than none.

**Size and sourcing:**
- 2–4 Q&As per page (smaller than the Homepage FAQ's 6–8 and the FAQ Page's full bank — this is a page-specific supplement, not a duplicate of either)
- Pull first from question-intent keywords already in that page's own cluster
- If the cluster has none but an obvious buyer question exists for this product/page type, write it — but don't manufacture keyword-less filler questions
- Never duplicate a question that already lives anywhere else on the site — homepage FAQ, the dedicated FAQ page, or another page's own mini-FAQ. Maintain a running registry of every question used as you build out each page's FAQ; if a question is already answered elsewhere, link to it from this page instead of re-answering it

**Answer rules:** same as below (Answer Rules, Non-Negotiable) — 40–65 words, concrete, no "it depends," include a keyword naturally, end with a link/CTA back into the page's own conversion path.

**Output location:** written into `keyword-map.md`'s Per-Page On-Page Requirements, in the new "Page-Level FAQ" field directly below that page's "FAQ Schema: Yes/No" flag (`output-formats.md` Document 1) — not a separate file, and not `faq-bank.md` (that file is homepage + dedicated-FAQ-page + blog-post FAQ content only).

**Schema:** FAQPage JSON-LD on the page itself (same block format as Schema Blocks below) — every page-level FAQ gets its own schema instance, not a shared one.

### Answer Rules (Non-Negotiable)
1. **Never answer "it depends"** — always give a concrete answer, then qualify if needed
2. **Include a keyword naturally** — don't force it, but every answer should contain a relevant phrase
3. **Include a link or CTA** — direct to a product, category, or related blog post
4. **Write for voice search** — answers should read naturally when spoken aloud
5. **Be authoritative** — write as the expert, not as someone guessing
6. **No fluff** — every sentence must add information
7. **40–65 word ceiling on all answers** — WebForge's AI extraction model and AEO standard both cap at 60–65 words. Answers longer than this risk not being extracted by AI assistants or appearing in featured snippets. Homepage FAQ: aim for 40–55 words. FAQ page: aim for 50–65 words. Never exceed 65 words in any answer.

### Schema Blocks
**FAQPage JSON-LD (for FAQ sections on any page):**
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "[Question text]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[Answer text — full, self-contained]"
      }
    }
  ]
}
```

**Speakable schema** — flag the single best answer on each page.
Use WebForge's class-based selector convention (never ID selectors — WebForge generates classes not IDs):
```json
{
  "@context": "https://schema.org",
  "@type": "WebPage",
  "speakable": {
    "@type": "SpeakableSpecification",
    "cssSelector": [".faq-answer-speakable"]
  }
}
```
WebForge adds `class="faq-answer-speakable"` to the best answer element during build. Flag in `faq-bank.md` which question gets this class per page.
