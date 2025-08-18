# PRD — Brand Brief Generation

## Objective
Generate a comprehensive brand brief for any e-commerce brand using multi-source research from MCP servers (Firecrawl, Tavily, Perplexity; optional Apify) **plus structured customer review datasets (CSV)**.  
Output must synthesize customer psychology, market positioning, emotional drivers, competitor analysis, and a funnel-aligned messaging plan into a single actionable document.

---

## Inputs (Centralized)
- **`/docs/brand_sources.md`** — canonical list of brand URLs (site, PDPs, socials, press, marketplaces).  
- **`/data/brand_reviews/{{BRAND_NAME}}_reviews.csv`** — structured review dataset (text, rating, source, author).  
- Optional: competitor seeds / discovery keywords inside `brand_sources.md`.  
- **Run date + brand** (used for output folder naming): `{{YYYY-MM-DD}}` and `{{BRAND_NAME}}`.

> **All prompts read from `brand_sources.md` and `/data/brand_reviews/*.csv` automatically.**  
> No pasting URLs or review text directly into prompts.

---

## Context Cache (Summaries)
- **`/docs/brand_context.md`** — running, *lightweight* summaries appended by Prompts 1–4 (≤2 pages per section).  
  Used as a fast lens, not as the sole data source.

---

## Tools & Responsibilities (MCP)
- **Firecrawl**: crawl the brand site (homepage, about, product pages, FAQs, PDPs). Extract positioning, claims, proof, tone, and structured product info.  
- **Tavily**: targeted web search for competitors, reviews, press, and third-party commentary.  
- **Perplexity**: synthesize/triangulate insights across UGC and open web; cluster patterns; generate comparisons.  
- **Apify (optional)**: only when the category is **review/marketplace/social heavy** (Amazon, Trustpilot, Judge.me, YouTube/TikTok/IG comments) or Firecrawl can’t fetch reliably.  
- **CSV Reviews Parser**: always ingest `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` if present. Extract and rank:  
  - Recurring phrases (frequency + emotional intensity)  
  - Sentiment (positive/negative/neutral, by theme)  
  - Figurative language, metaphors, identity conflicts  
  - Differences pre-purchase vs post-purchase

---

## Output Structure & Persistence (Detailed + Summary)

### Per-Prompt Detailed Outputs
All detailed outputs saved to:
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/
01_deep_customer_voice_research_output.md
02_competitive_landscape_output.md
03_purchase_motivation_framework_output.md
04_messaging_funnel_strategy_output.md

### Per-Prompt Summaries
Each prompt also **appends a concise summary** to:
/docs/brand_context.md

---

## Final Brief (assembled from 01–04)
1. **Brand Overview**  
2. **Customer Segmentation & Psychology** (ICPs, VoC, emotional drivers; including CSV-derived insights)  
3. **Market Landscape** (direct/indirect competitors; pricing/offers; positioning gaps)  
4. **Voice of Customer** (pain points, desires, exact language with sources; clear [Customer Reviews CSV] vs [External Web Sources] attribution)  
5. **Messaging Framework** (pillars, emotional drivers, do’s/don’ts, headline starters)  
6. **Funnel Content Strategy** (awareness/consideration/conversion/retention)  
7. **Opportunities & Risks**

---

## Requirements
- **Source Attribution:**  
  - Reviews from CSV must be explicitly tagged `[Customer Reviews CSV]`.  
  - External forums, blogs, press, etc. tagged `[External Web Sources]`.  
  - Brand seeds tagged `[brand_sources.md]`.  
- **Minimize hallucination:** prefer tool outputs + CSV reviews.  
- **Assumption Marking:** when uncertain, mark as *Assumption* and propose a verification step.  
- **Reproducible:** if rerun with same sources/date, outputs and folder paths match.  
- **Formatting:** clean Markdown; distinct sections.

---

## Success Criteria
- A marketing team could launch campaigns using only the brief.  
- Balanced qualitative (voice/emotions) + quantitative (competitive facts).  
- **CSV reviews leveraged as a primary VoC dataset**, not supplemental.  
- No critical section missing; sources clearly attributed.  
- **All four detailed outputs present** in `/outputs/{{date}}_{{brand}}/` + summaries appended to `brand_context.md`.