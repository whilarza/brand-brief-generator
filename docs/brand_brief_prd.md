# PRD — Brand Brief Generation

## Objective
Generate a **comprehensive brand brief** for any e-commerce brand using only **MCP server outputs** (Firecrawl, Tavily, Perplexity; optional Apify) **plus structured customer review datasets (CSV)**.

The final brief must synthesize:
- Customer psychology & Voice of Customer (VoC)
- Market positioning & competitor landscape
- Emotional drivers, objections, and unmet needs
- Messaging framework & funnel-aligned content strategy

The output should be directly usable by a marketing team to launch campaigns.

---

## Inputs (Centralized)
- **`/docs/brand_sources.md`** — canonical list of brand URLs (site, PDPs, FAQs, socials, press, marketplaces); may include competitor seeds/keywords.
- **`/data/brand_reviews/{{BRAND_NAME}}_reviews.csv`** — structured reviews (text, rating, source, author, date if available).
- **Run metadata**: `{{YYYY-MM-DD}}` and `{{BRAND_NAME}}` (used for folder naming and headers).

> 🔒 **Rule:** All prompts must pull from **MCP outputs** and **CSV datasets**. Do **not** rely on “general model knowledge” or default web search.

---

## Context Cache (Summaries)
- **`/docs/brand_context.md`** — lightweight rolling summaries appended by Prompts 01–04.  
  - Max length **≤ 2 pages per prompt section**.  
  - Used as a quick lens only; **downstream prompts must reference the full detailed outputs**.

---

## Tools & Responsibilities (MCP)
- **Firecrawl MCP**  
  Crawl brand site (homepage, about, PDPs, FAQs, blog). Extract **positioning, claims, tone, proof, structured product info**.
- **Tavily Remote MCP**  
  Targeted web/search for **competitors, reviews, press, third-party commentary**. Return diverse, reputable domains.
- **Perplexity MCP**  
  **Synthesis & triangulation** across UGC and open web; cluster recurring patterns; perform contradiction checks; generate comparisons.
- **Apify (optional)**  
  Use when category is **review/marketplace/social-heavy** (Amazon, Trustpilot, Judge.me, YouTube/TikTok/IG) or if Firecrawl cannot fetch reliably.
- **CSV Reviews Parser (local)**  
  Always ingest `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` if present to extract and rank:
  - Recurring phrases (**frequency × emotional intensity**)
  - Sentiment (pos/neg/neutral) grouped by theme
  - Figurative language, metaphors, identity conflicts
  - Differences **pre-purchase vs post-purchase**

> ❗ **MCP Enforcement:** Default web search is **not permitted**. If an MCP call fails, note it explicitly (see *Failure Handling*).

---

## Output Structure & Persistence

### Per-Prompt Detailed Outputs (must exist)
Saved to:
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/
01_deep_customer_voice_research_output.md
02_comp_landscape_positioning_output.md
03_purchase_motivation_framework_output.md
04_messaging_pillars_content_strategy_output.md

Each detailed output **must include**:
- Header with:
  - **Brand:** `{{BRAND_NAME}}`
  - **Date:** `{{YYYY-MM-DD}}`
- Prompt-specific structured sections (see Minimum Detail Requirements)
- **Source Traceability** section (end of file)

### Per-Prompt Summaries (context cache)
Append to:
/docs/brand_context.md

- Max **≤ 2 pages** per prompt
- Keep to key findings; avoid raw dumps

### Persistence Rules
- No overwrites; always **append by date**.
- Folder naming is standardized:  
  `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`
- Filenames follow the list above exactly.

---

## Minimum Detail Requirements (per prompt)

### Prompt 01 — Deep Customer & Voice Research
- **ICPs:** 3 profiles (Strangers / Aware-non-buyers / Customers)
  - Each ICP: **≥ 3 emotional drivers**, **≥ 3 fears/objections**, **≥ 1 identity conflict**, **≥ 3–5 quotes** (mix pos/neg), **triggers & language at moment-of-need**
- **VoC Phrases:** **≥ 20–30** recurring phrases/quotes **ranked** by frequency × intensity (combine CSV + external web)
  - Tag sources: `[Customer Reviews CSV]` vs `[External Web Sources]`
- **Themes:** Metaphors, figurative language, identity tensions, emotional consequences of inaction
- **Unmet Needs & Risks:** Price sensitivity, stability/durability, piece-count vs build size, warranty/support (if found)

### Prompt 02 — Competitive Landscape & Positioning
- **Direct competitors:** **≥ 5**
- **Indirect competitors:** **≥ 3**
- For each key competitor (≥ 5): positioning claim(s), proof/evidence, notable offer/pricing, differentiators vs brand
- **Positioning gaps & opportunities:** explicit list (≥ 5 items)
- **Offer & pricing patterns:** clear comparison table or bullets

### Prompt 03 — Purchase Motivations & Brand Framework
- **Motivations:** **≥ 5** (mapped to VoC drivers)
- **Objections:** **≥ 5** (with rebuttal levers)
- **Emotional drivers:** **≥ 3** tied to framework elements
- **Brand Framework:** pillars/values/RTBs (reasons-to-believe) grounded in Prompt 01–02 evidence

### Prompt 04 — Messaging Pillars & Content Strategy
- **Core pillars:** **≥ 3** pillars, each with **≥ 2** sub-points and VoC support
- **Do/Don’t guardrails:** per pillar (tone, claims, sensitivities)
- **Funnel mapping:** Awareness / Consideration / Conversion / Retention — **concrete content ideas** per stage (≥ 3 per stage), with callouts for **reviews-driven** assets and **counter-objection** assets

---

## Final Brief (assembled from 01–04)
1. **Brand Overview**
2. **Customer Segmentation & Psychology**  
   (ICPs, VoC, emotional drivers; CSV + external sources)
3. **Market Landscape**  
   (direct + indirect competitors; positioning gaps; pricing/offer comparisons)
4. **Voice of Customer**  
   (pain points, desires, exact quotes with source tags)
5. **Messaging Framework**  
   (pillars, emotional do’s/don’ts, headline starters)
6. **Funnel Content Strategy**  
   (mapped to awareness, consideration, conversion, retention)
7. **Opportunities & Risks**  
   (gaps, tensions, threats; explicit watch-outs)

---

## Requirements

### Source Attribution (mandatory tags)
- CSV reviews → **`[Customer Reviews CSV]`**
- External forums/blogs/press → **`[External Web Sources]`**
- Brand seeds → **`[brand_sources.md]`**

### Failure Handling (never silent)
If any MCP/tool fails or data is missing, include a visible note in the deliverable:
[MISSING DATA: Firecrawl retrieval error on {{url or topic}}]
[MISSING DATA: Tavily query error on {{query}}]
[MISSING DATA: Perplexity synthesis unavailable]
[MISSING DATA: /data/brand_reviews/{{BRAND_NAME}}_reviews.csv not found]

Proceed with available sources and clearly state implications on confidence/coverage.

### Assumption Marking
If any content is inferred (not directly evidenced), tag it as **_Assumption_** and propose a **verification step** (specific source to check or query to run).

### Formatting
- Clean, consistent **Markdown**
- Use headings, lists, tables where helpful
- Keep quotes verbatim where possible (or clearly paraphrased)

### Validation Before Save
- Ensure headers include **Brand** and **Date**
- Ensure **Source Traceability** section exists (with link text or path references)
- Ensure minimum counts are met; if not, add an explicit **[LIMITATION]** note

---

## Success Criteria
- A marketing team can **launch campaigns using only the brief**.
- Balanced qualitative (VoC/emotions) and quantitative (competitor facts).
- **CSV reviews leveraged as a primary dataset**, not optional.
- **All four detailed outputs present** in `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`, and summaries appended to `brand_context.md`.
- Minimum detail thresholds met (or limitations clearly logged).
- No fabrication; all critical claims supported by sources or labeled as assumptions.

---