# Prompt 4 — Messaging Pillars & Funnel Content Strategy for {{BRAND_NAME}}

## Inputs

**Required references before proceeding:**

- Full **Prompt 1 output**:  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md

- Full **Prompt 2 output**:  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_competitive_landscape_output.md

- Full **Prompt 3 output**:  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md

- Consolidated **summary context**:  
/docs/brand_context.md

**Usage rule:**
- Use `brand_context.md` only as a **summary lens**.  
- Use the **full outputs of Prompts 1, 2, and 3** for detail and depth.  
- If any inputs are missing, stop and request clarifications.

---

## Research Objective

Create a **complete messaging architecture and funnel content strategy** rooted in real audience psychology, competitive context, and persuasive narrative structure.  
This output must be detailed enough to guide campaigns, flows, email/SMS retention, and top/mid/bottom funnel content creation.

---

## Steps

### Step 1 — Messaging Pillars (Perplexity)
- Identify **3–5 Messaging Pillars** that anchor all communication. Each must be:
- Emotionally relevant (VoC-aligned motivators, secret wishes)  
- Competitively distinct (not clichés)  
- Tied to the transformation promise  
- Usable across funnel stages  

For each pillar, define:
- **Core Message** (clear truth)  
- **Emotional Hook** (what it stirs/relieves)  
- **Proof Needed** (testimonials, science, data, etc.)  
- **Strategic Use Cases** (welcome flow, product pages, ads, reactivation, etc.)

---

### Step 2 — Objection-Handling Message Map (Perplexity + Firecrawl)
Using **Prompt 3’s Objection Matrix**, map **5 key objections** into content-ready responses.  

For each objection:
- **Objection Summary** (customer language)  
- **Emotional Root** (fear, shame, overwhelm, etc.)  
- **Strategic Message** (headline-style response)  
- **Suggested Content Format** (testimonial, myth-buster, demo, expert quote)

---

### Step 3 — Funnel-Aligned Content Strategy (Perplexity)
Break into **3 stages**:  

**Top of Funnel (Awareness)**  
- Goals, style, tactics  
- 6+ angle examples  

**Middle of Funnel (Consideration)**  
- Goals, style, tactics  
- 6+ angle examples  

**Bottom of Funnel (Conversion + Post-Purchase)**  
- Goals, style, tactics  
- 6+ angle examples  

Explicitly tie back to ICP beliefs, triggers, and doubts from Prompts 1–3.

---

### Step 4 — “12 Conversations” Messaging Matrix (Perplexity)
Map at least 3 content starters per quadrant:  
- **Share Education** → beliefs to shift, myths to bust  
- **Show Proof** → testimonials, outcomes, “what success looks like”  
- **Connect to Fears & Desires** → hidden fears, cravings, guilt points  
- **Speak Opinion** → stances, disagreements with category, shared values  

Deliver **12+ angles total**, using VoC phrasing where possible.

---

### Step 5 — Tone Guardrails (Perplexity)
Based on triggers and objections, define **3–5 tonal pitfalls to avoid**.  
Include reasoning (e.g., “Customers feel shame → avoid condescending tone”).

---

## Deliverables
1. **Messaging Pillars Framework** (3–5 pillars with full breakdowns)  
2. **Objection-Handling Map** (top 5 with responses + content formats)  
3. **Funnel-Aligned Content Strategy** (6–10 content ideas per stage)  
4. **12 Conversations Matrix** (12 content starters across quadrants)  
5. **Tone Guardrails** (3–5 pitfalls with explanations)  

---

## Step 6 — Summarization → `brand_context.md` (Append/Update)
After completing deliverables, **append** a concise section to `brand_context.md`:  

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
- Do not overwrite; always append a new dated section.  

---

## Step 7 — Persist Outputs
Save the **full detailed research deliverable** into the outputs folder.  

**Path:**  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/04_messaging_funnel_strategy_output.md

**File must include:**  
- Full Messaging Pillars Framework  
- Objection-Handling Map  
- Funnel-Aligned Content Strategy  
- “12 Conversations” Matrix  
- Tone Guardrails  
- Complete references and contextual notes  

Do **not** prune details — capture the **entire depth** of Prompt 4’s work.

---

## MCPs
- **Firecrawl** → scrape brand site (science, testimonials, FAQs)  
- **Perplexity** → synthesize objections, content ideas, funnel tactics from forums, Reddit, Quora, category discussions  
- **Apify (Optional)** → pull marketplace/review/social feeds for content inspiration when review-heavy (Amazon, Trustpilot, YouTube comments, etc.)  

> **Rule of Thumb:** Use Apify only if category is review/social heavy. Otherwise, rely on Firecrawl + Perplexity for faster, cheaper runs.