# Prompt 4 — Messaging Pillars & Funnel Content Strategy for {{BRAND_NAME}}

## Inputs

**Required references before proceeding:**

- Full **Prompt 1 output**:  
  `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md`

- Full **Prompt 2 output**:  
  `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_competitive_landscape_output.md`

- Full **Prompt 3 output**:  
  `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md`

- Consolidated **summary context**:  
  `/docs/brand_context.md`

**Usage rule:**
- Use `brand_context.md` only as a **summary lens**.  
- Use the **full outputs of Prompts 1, 2, and 3** for depth and detail.  
- If any inputs are missing, **stop and request clarifications** before proceeding.  

---

## Inputs/Instruction for Cursor

1. Validate that all required input files exist before continuing:  
   - `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md`  
   - `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_competitive_landscape_output.md`  
   - (and for Prompt 4, also Prompt 3’s output)  

2. If any required input file is missing, stop and return:  
   `"Missing input(s). Please ensure all required prior outputs are generated before running this prompt."`

3. Only proceed once all required files are confirmed.  

---

## Report Header Standard

Always begin the report with:

**Date:** {{RUN_DATE}}  
**Brand:** {{BRAND_NAME}}  

- If `RUN_DATE` is not explicitly passed, parse it from the output folder path `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`.  
- Never take the date or brand name from examples, sources, or defaults.  

---

## Research Objective

Create a **complete messaging architecture and funnel content strategy** rooted in:  
- **Audience psychology** (Prompt 1)  
- **Competitive positioning** (Prompt 2)  
- **Purchase motivations and objections** (Prompt 3)  

This output must be detailed enough to guide:  
- Campaigns  
- Automated flows  
- Email/SMS retention  
- Top/Mid/Bottom funnel content creation  

---

## Steps

### Step 1 — Messaging Pillars (Perplexity + Firecrawl enforced)
Identify **3–5 Messaging Pillars** that anchor all brand communication.  

**Rules:**  
- Each must tie directly to **Prompt 1 (VoC motivators)**, be competitively distinct using **Prompt 2**, and address transformations from **Prompt 3**.  
- For each pillar, **provide all fields in a table**:  

| Core Message | Emotional Hook | Proof Needed | Strategic Use Cases |
|--------------|---------------|--------------|---------------------|
| Fill this with detail. Minimum 3–4 sentences each cell. Reference VoC phrases from Prompt 1. |

---

### Step 2 — Objection-Handling Message Map (Perplexity + Firecrawl enforced)
Using **Prompt 3’s Objection Matrix**, map **5 key objections** into content-ready responses.  

**Rules:**  
- Always cite the **Emotional Root** (fear, doubt, shame, overwhelm, etc.).  
- Tie objections back to **Prompt 1 language** + **Prompt 2 competitor claims**.  
- Present results in a table format:  

| Objection Summary (customer language) | Emotional Root | Strategic Message (headline-style) | Suggested Content Format | Proof Source / VoC Reference |
|---------------------------------------|----------------|-----------------------------------|--------------------------|------------------------------|
| Fill each cell with detail. Minimum 2–3 sentences. |

---

### Step 3 — Funnel-Aligned Content Strategy (Perplexity + Firecrawl enforced)
Break into **3 funnel stages**, and for each, provide:  

- **Goals** (conversion aim at this stage)  
- **Style & Tactics** (messaging type + channel approach)  
- **6+ Content Angles**, each including:  
  - **Headline/Hook**  
  - **Explanation (2–3 sentences)**  
  - **Proof Source or VoC tie-in**  

**Stages:**  
- **Top of Funnel (Awareness)**  
- **Middle of Funnel (Consideration)**  
- **Bottom of Funnel (Conversion + Post-Purchase)**  

---

### Step 4 — “12 Conversations” Messaging Matrix (Perplexity)
Map at least **3 content starters per quadrant** (12 minimum).  

| Quadrant | Example Starter | Explanation (2–3 sentences) | VoC/Proof Source |
|----------|----------------|-----------------------------|------------------|
| Share Education | … | … | … |
| Show Proof | … | … | … |
| Connect to Fears & Desires | … | … | … |
| Speak Opinion | … | … | … |

---

### Step 5 — Tone Guardrails (Perplexity)
Define **3–5 tonal pitfalls to avoid** based on triggers and objections.  

For each:  
- State the **pitfall clearly**  
- Give **reasoning tied to ICP psychology** (from Prompts 1–3)  
- Suggest a **preferred alternative style**  

Deliver as a bulleted list with explanations.  

---

## Evidence Quotas & Iterate
- Do not finalize until **ALL** apply:
  - `CITATIONS >= MIN_CITATIONS`
  - `DIRECT_QUOTES >= MIN_DIRECT_QUOTES`
  - If Reddit/YouTube are available: `REDDIT_QUOTES >= MIN_REDDIT_QUOTES` and `YT_TRANSCRIPTS >= MIN_YT_TRANSCRIPTS`
  - Prompt 2 only: `COMPETITORS >= MIN_COMPETITORS`
- If any quota is unmet, **generate targeted follow-up queries** and repeat retrieval/synthesis up to `MAX_ITERATIONS` or until quotas pass.
- Log remaining gaps in a **[LIMITATIONS]** section with next best queries to run.

---

### Step 6 — Iteration Clause (Critical)
After completing each step:  

1. **Review depth**: If any section has fewer than the required details (sentences, examples, proof points), expand automatically.  
2. **Cross-check**: Ensure every step cites inputs from **all three prior prompts**. If not, revise.  
3. **Loop**: Rerun expansion until all sections are comprehensive, clear, and evidence-backed. Do not move forward until quality is met.  

---

## Deliverables

1. **Messaging Pillars Framework** (table format with detail)  
2. **Objection-Handling Map** (table format with detail)  
3. **Funnel-Aligned Content Strategy** (minimum 6 content angles per stage, detailed)  
4. **12 Conversations Matrix** (12+ detailed starters across quadrants)  
5. **Tone Guardrails** (3–5 with reasoning + alternatives)  

---

## Copywriter Synthesis Pass (Mandatory)
Create a **one-page, narrative-style brief** for the creative team:
- Write in **customer language**; keep quotes verbatim where possible.
- Include **3 hook-ready headlines** per ICP.
- Provide **5 objection-handling lines** (headline + 1-sentence proof).
- Add a **Do/Don’t tone guide** (5 bullets each) tied to emotional triggers.
Save as:  
`/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/0X_copywriter_synthesis.md`

---

## Step 7 — Summarization → `brand_context.md` (Append/Update)

After completing deliverables, append a concise section to `brand_context.md`:  

**Title:**  
[Prompt 4] Messaging & Funnel Summary — YYYY-MM-DD  

**Include:**  
- 3–5 Messaging Pillars  
- Top objections + response themes  
- 3–5 Funnel strategy highlights  
- 12 Conversations overview  
- 2–3 Tone pitfalls  

**Rules:**  
- Keep summary ≤ 2 pages.  
- Do not overwrite; always append as a new dated section.  

---

## Step 8 — Persist Outputs

Save the **full detailed research deliverable** into the outputs folder:  

/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/04_messaging_funnel_strategy_output.md

**File must include:**  
- Full Messaging Pillars Framework  
- Objection-Handling Map  
- Funnel-Aligned Content Strategy  
- “12 Conversations” Matrix  
- Tone Guardrails  
- Complete references and contextual notes  

**Validation before saving:**  
- Ensure header contains:  
  - **Date:** {{RUN_DATE}}  
  - **Brand:** {{BRAND_NAME}}  
- If not, correct automatically.  

---

## MCPs

- **Firecrawl** → scrape brand site (science, testimonials, FAQs)  
- **Perplexity** → synthesize objections, angles, funnel tactics from forums, Reddit, Quora, category discussions  
- **Apify (Optional)** → pull marketplace/review/social feeds for content inspiration when review-heavy (Amazon, Trustpilot, YouTube, etc.)  

> **Rule of Thumb:** Use Apify only if category is review/social heavy. Otherwise, rely on Firecrawl + Perplexity for faster, cheaper runs.