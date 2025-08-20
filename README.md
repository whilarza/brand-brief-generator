# Brand Brief Generator

**Comprehensive e-commerce brand brief generation using AI-powered MCP servers and customer review datasets**

Generate campaign-ready marketing briefs that synthesize customer psychology, market positioning, emotional drivers, and messaging frameworks - all from structured web crawling and CSV review data.

## Objective

Create comprehensive brand briefs for any e-commerce brand using MCP server outputs (Firecrawl, Tavily, Perplexity; optional Apify) plus structured customer review datasets (CSV). The final brief must be directly usable by a marketing team to launch campaigns.

## What It Generates

**Customer Psychology & Voice of Customer (VoC)** - 3 ICP profiles with emotional drivers, fears, objections, and identity conflicts. 20-30 recurring phrases ranked by frequency and intensity, tagged by source.

**Market Positioning & Competitor Landscape** - 5+ direct competitors, 3+ indirect competitors with positioning claims, proof, pricing patterns, and differentiation opportunities.

**Emotional Drivers & Purchase Motivations** - 5+ motivations mapped to VoC drivers, 5+ objections with rebuttal levers, emotional framework grounded in evidence.

**Messaging Framework & Content Strategy** - 3+ core pillars with VoC support, funnel-aligned content for awareness/consideration/conversion/retention stages.

## Inputs Required

**Brand Sources** - `/docs/brand_sources.md` with brand URLs (site, PDPs, FAQs, socials, press, marketplaces) and competitor seeds.

**Customer Reviews** - `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` with structured review data (text, rating, source, author, date).

**MCP Servers** - Firecrawl (brand site crawling), Tavily (targeted web search), Perplexity (synthesis & triangulation), Apify (optional for review-heavy categories).

## Output Structure

**Detailed Reports** - 4 comprehensive files in `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/` with source traceability and minimum detail requirements.

**Context Summaries** - Lightweight rolling summaries in `/docs/brand_context.md` (≤2 pages per prompt) for quick reference.

**Final Brief** - Assembled brand overview, customer segmentation, market landscape, VoC, messaging framework, funnel strategy, and opportunities/risks.

## Success Criteria

Marketing teams can launch campaigns using only the brief. Balanced qualitative (VoC/emotions) and quantitative (competitor facts). CSV reviews leveraged as primary dataset. All four detailed outputs present with minimum detail thresholds met. No fabrication; all claims supported by sources.

---

*Built for marketing teams who need comprehensive, evidence-backed brand briefs in hours, not weeks.*
