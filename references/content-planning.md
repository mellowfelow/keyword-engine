# Content Planning Reference

## Blog Planning Rules

### Who Gets a Blog Post
Every cluster mapped to "new blog post" in Phase 5 gets a full brief. Additionally:
- Any informational cluster with Vol 100+ that didn't match an existing page → blog post
- Any commercial cluster with 3+ keywords that didn't map to a product/category page → blog post
- Any comparison keyword cluster → blog post (never a product page)
- Maximise the number of posts: if a cluster is viable, write the brief

### ⭐ Minimum 20 Fully-Briefed Posts, Day One — Plus a Growing Backlog

**Every session must deliver at least 20 complete blog briefs, ready to build immediately** — not trickled out over the 12-week calendar, all 20 written and in blog-plan.md before the session ends. Beyond that floor, keep planning: queue every additional viable topic as a future-backlog entry in keyword-cluster.txt (see Content Calendar below) rather than stopping at 20. The floor is a minimum, not a target.

**If the natural clusters from Phase 4/5 don't reach 20**, expand the topic pool using the same principle as Secondary Keyword Supplementation (filter-and-cluster.md) — real data first, generated topics only to fill the gap:

1. **Broaden informational coverage first.** Re-scan the Supporting Pool for informational/question-intent keywords that didn't cluster tightly enough to be picked up in Phase 4 — these make perfectly good standalone posts even as a smaller (2–4 keyword) cluster.
2. **Site-search query mining, if a site-search export was provided.** Real first-party queries on informational/question topics (not just product searches) are direct evidence of what visitors want to read, not just buy — mine the same export used for secondary supplementation (filter-and-cluster.md) for topic angles, not just keywords.
3. **Competitor content gaps, if a competitor SEMrush export was provided.** Any informational/commercial keyword the competitor ranks for that this site has no blog coverage of at all is a real, evidenced topic — cross-reference against the Competitor Gap Analysis output (product-gaps.md) rather than re-deriving it separately.
4. **Derive topics from the product catalog.** Every product category reasonably supports a "how to choose," "how to maintain," "buying guide," and "FAQ roundup" post even without a matching keyword in the export — these are genuine, useful topics inferred from what the site sells, not invented filler. Label them clearly as catalog-derived rather than export-backed.
5. **Google related searches, applied to topics not just keywords.** Pull related-search and "people also ask" data for the site's core product/category terms and mine it for blog-worthy angles the original export didn't surface.
6. **Comparison and accessory angles.** Every competitor brand in the Competitor Brands list supports a comparison post (Phase 1); every accessory/part pattern (product-gaps.md § Accessory Gap Detection) supports a "do I need X" or "how to choose X" post.

**Never pad with genuinely content-less topics just to hit 20.** If the niche is so narrow that even catalog-derived and comparison angles can't reach the floor, ship what's real and say so plainly in the session summary — e.g. "17 fully-briefed posts delivered; niche breadth doesn't support more without content-less padding" — rather than inventing a post with nothing to say. This is the same honesty principle as the secondary-keyword floor: a stated shortfall with a reason beats a silently padded number.

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

### Funnel Position
- **Bottom of funnel (buy now):** Comparison posts, reviews, "best X for [buyer type]" → publish first
- **Middle of funnel (considering):** Buyer's guides, "how to choose X", feature explainers → publish second
- **Top of funnel (awareness):** General educational content, "what is X" → publish last

---

## Full Blog Brief Template

For every blog post, output this complete brief:

```markdown
## Blog Brief: [Post Title]

**URL Slug:** /blog/[slug]/
**Funnel Position:** Bottom / Middle / Top
**Priority Tier:** T1 / T2
**Content Type:** Listicle / Comparison / How-To / Review / Explainer / Guide
**Target Word Count:** [number]
**Schema Type:** Article / HowTo / FAQPage / Review

---

### Keywords
- **Primary:** [keyword] (Vol: X, KD: X)
- **Secondary:** [kw1], [kw2], [kw3], [kw4], [kw5]
- **LSI/Supporting:** [list from T3 pool]

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

**The 12-week calendar is the visible planning window, not a cap on total output.** With a 20+ post minimum, the full backlog routinely extends well past week 12 — everything beyond the 12-week window still gets a full brief (per the minimum-20-plus-as-many-as-viable rule above) and queues in keyword-cluster.txt as `[UNUSED]` for WebForge to pull once the first 12 weeks are built. Sequence into the calendar:

```markdown
## 12-Week Content Calendar (first window — backlog continues beyond week 12 in keyword-cluster.txt)

### Priority Logic
Week 1–4: All T1 Bottom-of-funnel posts (direct sales drivers)
Week 5–8: T1 Middle-of-funnel + T2 Bottom-of-funnel
Week 9–12: T2 Middle-of-funnel + T1/T2 Top-of-funnel
Beyond Week 12: remaining backlog, sequenced the same way (Bottom → Middle → Top, T1 before T2) — full list in keyword-cluster.txt, not repeated here

---

| Week | Post Title | Primary Keyword | Type | Funnel | Tier | Word Count |
|------|-----------|----------------|------|--------|------|-----------|
| 1 | [title] | [keyword] | [type] | Bottom | T1 | [words] |
| 2 | [title] | [keyword] | [type] | Bottom | T1 | [words] |
...

---

### Pillar Posts (produce in parallel, publish in Week 4, 8, 12)
These are long-form anchors — start writing them week 1, publish later so cluster posts are already live and can link to them.

---

### Backlog Beyond Week 12
**Total briefed:** [n] posts ([n] scheduled in the 12-week window, [n] queued beyond it)
All [n] backlog posts have complete briefs in this document — they're sequenced in keyword-cluster.txt, not held back for a future session.
```

---

## FAQ Rules

### FAQ Bank Structure
All question-intent keywords + question signals across all clusters feed here.

**Sources for FAQ questions:**
1. Keywords with question-format phrasing (does, can I, how long, will, should, is it)
2. Informational keywords that imply a question (e.g. "electric dirt bike age limit" → "What age can a child ride an electric dirt bike?")
3. Commercial keywords with doubt signals (e.g. "electric dirt bike worth it" → "Are electric dirt bikes worth the money?")

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

### Page-Level FAQ (product / category / brand hub / blog — every mapped page, not just homepage + FAQ page)

**The goal is organic keyword coverage.** A page-level mini-FAQ is indexable content unique to that page — it lets a product or category page compete for question-style long-tail queries it otherwise has zero shot at, without diluting the page's primary keyword focus the way stuffing more prose would. This is the single easiest way to widen organic traffic per page without adding new pages.

**When to add one:** whenever the mapped cluster (primary + secondaries + LSI) contains **2 or more question-intent keywords**, or the page-mapping process surfaced obvious buyer questions for that specific product/category/brand even without a literal question-format keyword in the data (e.g. a youth electric bike product page almost always needs an age/safety question even if "what age" wasn't in the export — use judgment, same as the niche-relevance rule).

**When to skip it:** a thin cluster with no question-intent signal and no obvious buyer question for that specific page. Don't invent a question just to check a box — an empty or filler FAQ is worse than none.

**Size and sourcing:**
- 2–4 Q&As per page (smaller than the Homepage FAQ's 6–8 and the FAQ Page's full bank — this is a page-specific supplement, not a duplicate of either)
- Pull first from question-intent keywords already in that page's own cluster
- If the cluster has none but an obvious buyer question exists for this product/page type, write it — but don't manufacture keyword-less filler questions
- Never duplicate a question that already lives anywhere else on the site — homepage FAQ, the dedicated FAQ page, or another page's own mini-FAQ. Maintain a running registry of every question used as you build out each page's FAQ; if a question is already answered elsewhere, link to it from this page instead of re-answering it

**Answer rules:** same as below (Answer Rules, Non-Negotiable) — 40–65 words, concrete, no "it depends," include a keyword naturally, end with a link/CTA back into the page's own conversion path.

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
