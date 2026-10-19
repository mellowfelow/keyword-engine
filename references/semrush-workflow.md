# Semrush/Platform Link — Operational Workflow

**This is the mechanism behind Rule 1 and Rule 4** (`core-rules.md`) —
every phase of this skill assumes real research is actually happening
against a real platform. This file is that "how."

## Scope — everything except Site Audit

Treat the link like Semrush, in full, **except its Site Audit section** —
that's a technical-SEO crawler tool (crawlability, broken links, Core Web
Vitals, HTTPS), not a keyword/taxonomy research concern; it belongs to
WebForge's own technical-SEO audit, not this skill. In scope here: Keyword
Magic Tool, Keyword Overview, Keyword Gap, Organic Research, AI
Visibility — anything that's actually keyword/competitor data.

## Target location — set first, every time

Every search sets the target location/database **before** running, never
after or skipped. This is `niche-taxonomy.md`'s "location always
user-stated upfront" rule, extended down to the literal tool-level
selector. A search run against the wrong database is as invalid as a
search run on stale data.

## Mandatory refresh-before-read — no exceptions

Per Rule 1's data-freshness addendum: **never read or record a keyword's
stats without refreshing/updating it first.** A keyword pulled without
refreshing doesn't count as checked — treat it the same as data that was
never looked at. **This applies to every single keyword, every time, in
every phase of this skill that sources keywords — no exceptions.** That
means Phases 1–9, every page type in `page-mapping.md`, and `niche-
taxonomy.md`'s own Step B research — not a partial list implying some
phases are exempt.

**A glitch or quota interruption mid-phase never risks a half-written
entry.** A page's `keyword-map.md` entry is only written once its research
is *complete* — an interruption simply means that phase hasn't finished
yet, so there's nothing premature to write or unwrite when work resumes.

## Refresh quota — 1000 per session, tracked actively

The platform allows **1000 keyword refreshes per session.** Keep a running
count in working session notes, incrementing per keyword refreshed, across
every phase/tool in this workflow (not reset per phase) — flag proactively
at ~950, not discovered by hitting a hard stop at 1000. When the quota is
exhausted: **stop, notify the user clearly, and wait** for them to refresh
the platform and provide a new link. Resume exactly where work left off —
never restart a phase from scratch just because the link changed mid-way.

## Glitch recovery — same protocol as quota exhaustion

The platform glitches often. When it does: **stop immediately, notify the
user**, and wait for them to refresh and provide a new link. Same
resume-don't-restart principle as the quota case — whatever research was
already completed and recorded (in `keyword-map.md`, `blog-plan.md`, etc.)
stays valid; only the *in-progress* step needs picking back up.

## Harvesting checklist — minimum comprehensive pass per niche/category

**Five sources, every time.** Each mapped to what it actually feeds:
- **Keyword Magic Tool → Topics view** — semantic clustering of the
  niche/category. Feeds topical-depth sourcing (category pages, Individual
  Brand pages in `page-mapping.md`) and `niche-taxonomy.md`'s taxonomy
  validation.
- **Keyword Magic Tool → Groups view** — SERP-pattern-based clustering.
  Feeds the clustering mechanics (`filter-and-cluster.md`, Phases 1–4) and
  cross-checks against cannibalisation risk early.
- **Keyword Overview → Questions tab** — question-based long-tail terms.
  Feeds Question-intent sourcing directly (the FAQ page, page-level
  mini-FAQs, blog H2 questions — `content-planning.md`).
- **AI Visibility page** — a Semrush *tool*, not to be confused with this
  skill's own `ai-visibility.md` reference file (that's on-page content/
  schema strategy, a distinct aspect). This page tracks which keywords
  actually trigger AI Overviews/AI-chatbot answers right now, and brand/
  competitor visibility within those answers. Feeds: (a) prioritization
  for the FAQ page's answer-first formatting — spend that effort first on
  keywords genuinely showing AI-Overview presence; (b) Rule 4's
  competitor touchpoints — which competitors are getting cited in AI
  answers for shared keywords is a real competitive signal on top of
  plain ranking data.
- **Keyword Gap / Organic Research** — a competitor's actual ranking-
  keyword profile. Feeds Rule 4's standing enrichment at all five of its
  touchpoints and `product-gaps.md`'s Competitor Gap Analysis directly —
  not reserved for when something comes up thin, run routinely, every pass.

Skipping any one of these five on a given research pass isn't a
shortcut — it's an incomplete harvest.

## Recommendations, from direct Semrush knowledge

- **Cross-check against Semrush's own Intent tags** (Transactional/
  Commercial/Informational/Navigational, shown in Keyword Magic Tool
  exports) as a first-pass sanity check before applying `filter-and-
  cluster.md`'s tie-break rules — not a replacement for the tie-break
  logic (which handles multi-signal keywords Semrush's own tagging
  doesn't), but a fast way to catch an obvious disagreement worth a second
  look.
- **Use the built-in SERP preview** (visible in Keyword Overview and
  Magic Tool) to run `filter-and-cluster.md`'s Situational Drop checks
  (marketplace-dominated SERP, non-commercial SERP for a nominally
  commercial keyword) directly, instead of a separate live search for the
  same information.
- **Use the trend graph** (Keyword Overview, 12-month view) for `niche-
  taxonomy.md`'s seasonality note and "is demand flat/growing, not dead"
  viability check — it's already the data source for that.
- **Consider Keyword Manager/Strategy Builder** (if the plan includes it)
  to organize the growing keyword set in-tool, mirroring this skill's
  phase structure (one list per phase/page type — homepage, categories,
  blog launch batch, blog reserve pipeline). This is a convenience mirror
  only — `keyword-map.md`'s Used-Keywords Registry remains the actual
  source of truth for cannibalisation checks, never replaced by in-tool
  organization.

## Quality Control — this file's own dedicated audit layer

Governed by Rule 5 (`core-rules.md`). A scope boundary, a location
discipline, a hard data-validity rule, a tracked quota, an interruption-
recovery protocol, and a five-source mandatory harvest are too much
distinct operational logic to leave as scattered shared-checklist bullets
— this file gets its own dedicated two-layer audit.

**Pre-ship checklist (run every research session using the link):**
1. **Scope** — Site Audit was never touched for keyword-engine purposes;
   everything else (Keyword Magic Tool, Keyword Overview, Keyword Gap,
   Organic Research, AI Visibility) was in bounds.
2. **Location** — set before every search this session, not after, not
   skipped, not left on a default/previous value.
3. **Refresh discipline** — every keyword read or recorded was refreshed
   first, with zero exceptions across every phase that sourced keywords
   this session, Phase 0 included.
4. **Quota** — a running count was actually kept (not estimated after the
   fact), flagged proactively near 950, never discovered by hitting 1000
   unexpectedly.
5. **Interruption recovery** — any glitch or quota exhaustion this session
   was met with immediate stop + notify, and work resumed exactly where it
   left off — no phase was restarted from scratch, and no half-written
   `keyword-map.md` entry resulted.
6. **Harvest completeness** — all five sources were pulled for every
   niche/category researched this session (Topics, Groups, Questions, AI
   Visibility, Keyword Gap/Organic Research) — none skipped, none
   demoted to optional.
7. **Tool-recommendation usage** — where applicable, Semrush's own Intent
   tags were cross-checked (not relied on as a replacement for the
   tie-break rules), the SERP preview was used for Situational Drop
   checks, and the trend graph was used for the seasonality/viability
   work, rather than re-deriving any of this via a separate search when
   the platform already had it on screen.

**Re-audit (later):**
- Has the platform's own tool layout, intent-tagging, or quota changed
  since the original research? Confirm the five-source harvest still
  works the way this file assumes before relying on it unchanged.
- Were any sessions in the interim affected by a glitch/quota event whose
  resume wasn't fully completed — a phase left genuinely half-researched
  across a session boundary, not just interrupted and then properly
  finished? Flag and complete it rather than assuming "resumed" meant
  "finished."
