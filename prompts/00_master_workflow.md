# 00_master_workflow.md  
**Master Orchestration Workflow for Brand Brief Generator**
---

## Execution Block (Run the Full Workflow)

**Command to Run in Cursor:**
/run 00_master_workflow.md

> This workflow implements the requirements defined in:  
> `/docs/brand_brief_prd.md`  
> Refer to that PRD for the full specification of objectives, tools, inputs, outputs, and success criteria.  
> This file focuses solely on execution order, context passing, and persistence.

---

## Purpose
Automate the full brand brief generation pipeline — from deep customer research through final messaging framework — using Prompts 01–04.  
Ensures all outputs are persisted in `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/` and summarized into `/docs/brand_context.md`.

---

## Pre-Check: Brand Review Data
Before running **Prompt 01**, check for existence of:

/data/brand_reviews/{{BRAND_NAME}}_reviews.csv

- **If present**: Pass this file as an **input dataset** to Prompt 01 (Deep Customer & Voice Research).  
- **If missing**: Proceed with Prompt 01 using only sources from `/docs/brand_sources.md`. Add a note to final deliverables that no review dataset was found.  

> Review CSV is always treated as a **first-class VoC source**. Prompts must tag quotes/insights from this dataset as `[Customer Reviews CSV]`.

---

## Execution Order
Run the following prompts in sequence.  
Each step both **writes a full detailed output** to the outputs folder **and** appends a **concise summary** to `/docs/brand_context.md`.

1. **Prompt 01 — Deep Customer & Voice Research**  
   - File: `/prompts/01_deep_customer_voice_research.md`  
   - Inputs:  
     - `/docs/brand_sources.md`  
     - `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` (if exists)  
   - Output:  
     `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md`

2. **Prompt 02 — Competitive Landscape & Positioning**  
   - File: `/prompts/02_comp_landscape_positioning.md`  
   - Output:  
     `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_comp_landscape_positioning_output.md`

3. **Prompt 03 — Purchase Motivations & Brand Framework**  
   - File: `/prompts/03_purchase_motivations_brand_framework.md`  
   - Output:  
     `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md`

4. **Prompt 04 — Messaging Pillars & Content Strategy**  
   - File: `/prompts/04_messaging_pillars_content_strategy.md`  
   - Output:  
     `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/04_messaging_pillars_content_strategy_output.md`

---

## Persistence Rules
- Each prompt saves its **full detailed output** in the dated brand folder under `/outputs/`.  
- Each prompt appends a **summary block** to `/docs/brand_context.md`.  
- Naming convention for full outputs:  
/outputs/{{YYYY-MM-DD}}{{BRAND_NAME}}/0X<prompt_shortname>_output.md

---

## Context Passing
- **Prompt 01 → Prompt 02–04**:  
Prompts 2–4 should reference the **full output file** from Prompt 1, not only the summary in `brand_context.md`.  
This ensures downstream prompts use the richest available data, including CSV reviews if present.  

- **Prompts 02–04**:  
May also reference `brand_context.md` for quick cross-prompt context.

---

## Error Handling & Source Notes
- If `brand_sources.md` has missing sections, proceed with available data but **note the gap** in deliverables.  
- If `brand_reviews.csv` is missing, note it explicitly in Prompt 1 deliverables.  
- Each full output must include a **source traceability section** with reference lists.  
- Failures in one step should not stop the workflow — mark the error and continue.

---

## Success Criteria (from PRD)
- A marketing team can use the combined outputs to launch campaigns.  
- Mix of qualitative (emotional drivers, VoC) and quantitative (competitive facts).  
- Outputs are cleanly structured, in Markdown, and free of fabrication.  
- CSV reviews leveraged when available.  
- Final outputs align with `/docs/brand_brief_prd.md` specifications.

---