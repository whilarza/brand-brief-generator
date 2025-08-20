# 00_master_workflow.md  
**Master Orchestration Workflow for Brand Brief Generator**  
---

## Run Metadata (single source of truth)
- **BRAND_NAME**: `{{BRAND_NAME}}`   <!-- replace at runtime -->
- **RUN_DATE**: `{{RUN_DATE}}`       <!-- YYYY-MM-DD; either auto from folder name or set manually -->

---

## Execution Block (Run the Full Workflow)

**Command to Run in Cursor:**  
/run 00_master_workflow.md

> This workflow implements the requirements defined in:  
> `/docs/brand_brief_prd.md`  
> Refer to that PRD for the full specification of objectives, tools, inputs, outputs, and success criteria.  
> This file focuses solely on execution order, MCP enforcement, context passing, persistence, and error-handling.

---

## Purpose
Automate the full brand brief generation pipeline — from deep customer research through final messaging framework — using Prompts 01–04.  
Ensures all outputs are persisted in `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/` and summarized into `/docs/brand_context.md`.

---

## Pre-Check: Brand Review Data
Before running **Prompt 01**, check for existence of:

/data/brand_reviews/{{BRAND_NAME}}_reviews.csv

- **If present**: Pass this file as an **input dataset** to Prompt 01 (Deep Customer & Voice Research).  
- **If missing**: Proceed with Prompt 01 using only sources from `/docs/brand_sources.md`. Add a note to final deliverables that no review dataset was found.  

> Review CSV is always treated as a **first-class VoC source**. Prompts must tag quotes/insights from this dataset as `[Customer Reviews CSV]`.

---

## MCP Enforcement (Global Rule)
All prompts (01–04) must use the following MCP servers for research and data enrichment:  
- **Firecrawl MCP** → crawling and structured extraction of brand sources  
- **Tavily Remote MCP** → contextual and category search  
- **Perplexity MCP** → synthesis, aggregation, and reasoning  

**Default web search is not permitted.**  
If MCP calls fail, outputs must explicitly state a `[MISSING DATA: MCP retrieval error]` section.

---

## Model Selection (Global Rule)

- All prompts (01–04) must explicitly specify a **model selection** at runtime.  
- **Default model recommendation:** `GPT-5` (for balanced quality, depth, and cost).  
- **When to use Max Mode:**  
  - Only enable Max Mode if the project requires very large context windows (>200k tokens), such as when attaching unusually long brand sources or multi-thousand review datasets.  
  - Be aware: Max Mode is slower and more expensive.  

### Future-Proofing Guidance
Because model availability and performance changes over time, this workflow does **not hardcode a single “best model.”**  
- Teams should review current model benchmarks and pricing quarterly.  
- Update this section if a newer model (e.g., GPT-5 successor, Claude Opus upgrade, Gemini Pro Max) offers better qualitative reasoning or cost-efficiency.  
- If uncertain, default to `Auto` mode in Cursor, which dynamically selects the best premium model available.

### Practical Rule of Thumb
- **Use GPT-5** for deep qualitative research (customer voice, emotional drivers, copywriting insights).  
- **Use Auto** if unsure — ensures Cursor optimizes for reliability and cost.  
- **Use Max Mode** only when the context window limit is a hard blocker.  

### Practical Model & Tool Tips
- **Model Selection by Prompt:**
  - **Prompts 1 & 2:** Use GPT-5 for depth and quality
  - **Prompts 3 & 4:** Use GPT-5 or GPT-5-fast (faster, still high quality)
- **Tool Optimization:**
  - Keep tools lean: enable only the servers you'll actually use for that brand
  - **Browserbase:** Enable only when Firecrawl/Apify fail or the page is JS heavy; pass specific URLs, not domains
  - **DataForSEO (dfs):** Whitelist just SERP/keywords/competitors endpoints; leave the rest disabled

---

## Research Orchestrator (Global)

**Goal:** emulate Deep Research with a repeatable loop: *Fan-out → Retrieve → Quality-gate → Enrich → Synthesize → Evaluate → Iterate.*

### Depth Controls (tunable)
- MIN_CITATIONS: 15           <!-- total unique domains across a prompt -->
- MIN_DIRECT_QUOTES: 18       <!-- verbatim or lightly paraphrased VoC -->
- MIN_REDDIT_QUOTES: 6        <!-- if Reddit MCP is enabled -->
- MIN_YT_TRANSCRIPTS: 2       <!-- if YouTube MCP is enabled -->
- MIN_COMPETITORS: 5          <!-- Prompt 2 requirement -->
- MAX_ITERATIONS: 3           <!-- agent loop upper bound -->
- GAP_RETRY: true             <!-- keep iterating until gaps close or limit hit -->

### Retrieval Plan (routing)
1) **Owned data (Firecrawl)** → site, PDPs, FAQ, blog, press.
2) **Open web (Perplexity)** → forums, reviews, third-party analysis with **citations**.
3) **Long-tail (Tavily/SerpAPI/Brave)** → fill holes the first pass missed.
4) **UGC (Reddit / YouTube)** → VoC depth; record direct quotes + links.
5) **Marketplaces (Apify)** → Amazon/Trustpilot/Judge.me when review-heavy.
6) **Escalation (Browserbase)** → if page is JS-rendered/infinite scroll or Firecrawl returns blank/truncated.

### Escalation Rules
- If **Firecrawl** response is empty, duplicated, or truncated → retry with **Apify**.
- If still incomplete **or** page is clearly JS-rendered (React/Vue/infinite scroll) → escalate to **Browserbase** and capture:
  - Rendered text,
  - First-screen screenshot,
  - URL + timestamp.
- Tag sources in outputs: `[Firecrawl]`, `[Perplexity]`, `[Tavily]`, `[SerpAPI]`, `[Brave]`, `[Apify]`, `[Browserbase]`, `[Reddit]`, `[YouTube]`, `[CSV]`.

### Quality Gates (must pass before synthesis)
- `CITATIONS >= MIN_CITATIONS`
- `DIRECT_QUOTES >= MIN_DIRECT_QUOTES` (mix of CSV, Reddit, marketplace, site testimonials)
- If Reddit/YouTube enabled: `REDDIT_QUOTES >= MIN_REDDIT_QUOTES` and `YT_TRANSCRIPTS >= MIN_YT_TRANSCRIPTS`
- Prompt 2 only: `COMPETITORS >= MIN_COMPETITORS`
- If gates fail and `GAP_RETRY = true` → generate **targeted follow-ups** (e.g., “pricing complaints”, “durability issues”, “return policy anxiety”) and rerun retrieval up to `MAX_ITERATIONS`.

### Evidence Ledger (saved alongside outputs)
- For each prompt, write `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/raw/evidence_0X.json` with:
  - `queries_run`, `tools_used`, `citations`, `quotes`, `screenshots`, `retries`, `gaps_remaining`.

---

## Execution Order
Run the following prompts in sequence.  
Each step must both **write a full detailed output** to the outputs folder **and** append a **concise summary** to `/docs/brand_context.md`.

### 1. Prompt 01 — Deep Customer & Voice Research
- **File:** `/prompts/01_deep_customer_voice_research.md`  
- **Inputs:**  
  - `/docs/brand_sources.md`  
  - `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` (if exists)  
- **Output:**  
/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md

### 2. Prompt 02 — Competitive Landscape & Positioning
- **File:** `/prompts/02_comp_landscape_positioning.md`  
- **Inputs:**  
- `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md`  
- `/docs/brand_context.md` (for summary continuity)  
- **Output:**  
/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/02_comp_landscape_positioning_output.md

### 3. Prompt 03 — Purchase Motivations & Brand Framework
- **File:** `/prompts/03_purchase_motivations_brand_framework.md`  
- **Inputs:**  
- `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md`  
- `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/02_comp_landscape_positioning_output.md`  
- `/docs/brand_context.md`  
- **Output:**  
/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md

### 4. Prompt 04 — Messaging Pillars & Content Strategy
- **File:** `/prompts/04_messaging_pillars_content_strategy.md`  
- **Inputs:**  
- All prior full outputs (`01`, `02`, `03`)  
- `/docs/brand_context.md`  
- **Output:**  
/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/04_messaging_pillars_content_strategy_output.md

---

## Persistence Rules
- Each prompt saves its **full detailed output** in the dated brand folder under `/outputs/`.  
- Each prompt appends a **summary block** to `/docs/brand_context.md`.  
- **Naming convention (standardized):**
/outputs/{{RUN_DATE}}{{BRAND_NAME}}/0X<prompt_shortname>_output.md

### Raw Evidence Persistence
- Alongside each prompt’s full output, save a machine-readable ledger:
  - Path: `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/raw/evidence_0X.json`
  - Contents: `queries_run`, `tools_used`, `citations`, `quotes`, `screenshots`, `retries`, `gaps_remaining`
- This ledger is used for QA and to reproduce runs.

---

## Summarization Guidelines (Global Rule)
- Each prompt must append a **concise summary ≤2 pages** into `brand_context.md`.  
- Summary should highlight **key findings only**, not raw data.  
- **Format:**  
[Prompt Title] — {{RUN_DATE}}
- Use bullets, short paragraphs, and direct phrasing.  

---

## Context Passing (Enforced)
- **Prompt 01 → Prompt 02–04**: Downstream prompts must always read the **full Prompt 01 output file** in addition to the summary.  
- **Prompt 02 → Prompt 03 → Prompt 04**: Each must reference the **full outputs** of all previous steps.  
- `brand_context.md` is used only for quick reference; it cannot replace the full files.  

---

## Error Handling & Source Notes
- If `brand_sources.md` has missing sections, deliverables must contain:  
[MISSING DATA: brand_sources.md incomplete]

- If `brand_reviews.csv` is missing, note it explicitly in Prompt 1 deliverables.  
- If any MCP server fails, deliverables must contain:  
[MISSING DATA: Firecrawl/Tavily/Perplexity retrieval error]

- Every full output must end with a **Source Traceability Section**, listing references and context used.  

---

## Success Criteria (from PRD)
- A marketing team can use the combined outputs to launch campaigns.  
- Balance of qualitative (emotional drivers, VoC) and quantitative (competitive facts).  
- Outputs are **detailed, structured in Markdown, and non-fabricated**.  
- CSV reviews leveraged when available.  
- Final outputs align with `/docs/brand_brief_prd.md` specifications.  
- Missing data is explicitly called out, never hidden.  

---