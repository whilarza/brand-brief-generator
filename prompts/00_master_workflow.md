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

yaml
Copy
Edit
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