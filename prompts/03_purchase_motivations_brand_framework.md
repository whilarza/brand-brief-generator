# Prompt 3 — Purchase Motivation, Objections & Brand Framework

## Inputs

**Required references before proceeding:**

- Full **Prompt 1 output**:  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md

- Full **Prompt 2 output**:  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_competitive_landscape_output.md

- Consolidated **summary context**:  
/docs/brand_context.md

**Usage rule:**
- Use `brand_context.md` only as a **summary lens**.  
- Use the **full outputs of Prompts 1 + 2** for depth and detail.  
- If any inputs are missing, stop and request clarifications.

---

### Report Header Standard
- Always use **RUN_DATE** and **BRAND_NAME** provided by the workflow.
- If RUN_DATE is not explicitly passed, parse it from the output folder path `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`.
- Never take the date or brand name from examples, sources, or defaults.

The report header must always begin:

**Date:** {{RUN_DATE}}  
**Brand:** {{BRAND_NAME}}

---

## Research Objective

Translate psychological, emotional, and competitive data into a **usable brand framework**.  
Define the emotional logic behind purchasing, uncover resistance points, and structure messaging that meets buyers with empathy and authority.

---

## Steps

### Step 1 — Motivation Map
For each segment (**Strangers, Audience Members, Customers**):
- Emotional motivators (fear, relief, pride, guilt, hope)  
- Logical motivators (ingredients, guarantees, ease-of-use, data)  
- Transformation Promise: outcome they believe they’re buying  
- Crisis/Catalyst: tipping moments from consideration → action  

Ground all motivators in **customer language** from Prompt 1.

---

### Step 2 — Objection Matrix
Identify 5–7 dominant objections. For each:  
- Statement in their own words (or close paraphrase)  
- Emotional root (fear of being duped, overwhelm, shame, etc.)  
- Logical surface reason (cost, complexity, trust, risk)  
- Strategic response (copy approach, proof element, education, offer)  

Be empathetic and practical — these are to be **used in live copy**.

---

### Step 3 — Brand Audience Framework
Answer with precision and emotional clarity:
- **WHO** – who is this for? (specific context, not generic)  
- **IDENTITY** – what labels/roles do customers assign themselves?  
- **SECRET WISH** – the unspoken outcome they desire most  
- **RELATIONSHIP** – how should they feel about {{BRAND_NAME}}? (guide, friend, protector, expert, rebel, etc.)  
- **POINT OF DIFFERENCE** – unique belief/stance that sets the brand apart  
- **VOICE** – 5 traits (e.g., warm, precise, empowering, irreverent)  
- **PROBLEM** – core emotional/practical problem solved  
- **AWARENESS** – life moment that surfaces the problem  
- **TRANSFORMATION** – change they will feel after success with {{BRAND_NAME}}  

---

### Step 4 — Funnel Mindset Map
Map beliefs, fears, and trust triggers at each stage:

**Top of Funnel (Strangers):**  
- What they believe/misunderstand  
- What they fear/avoid  
- What they’re open to hearing  

**Middle of Funnel (Audience Members):**  
- What they wrestle with  
- Questions they ask  
- What builds/breaks trust  

**Bottom of Funnel (Customers/Post-Purchase):**  
- What they hope will happen  
- Lingering doubts  
- Messages that turn them into advocates  

---

### Step 5 — Brand Tone Risk Map
List 3–5 tonal red flags to avoid.  
Each should connect to an emotional driver or objection (e.g., if shame → avoid preachy tone).

---

### Step 6 — Summarization → `brand_context.md` (Append/Update)
After completing deliverables, **append** a concise section to `brand_context.md`:

**Title:**  
[Prompt 3] Motivation, Objections & Framework — YYYY-MM-DD

**Include:**  
- 5–7 core motivators (emotional + logical)  
- Top objections + response themes  
- Brand Framework (Promise, Proof, Personality, Principles)  
- 3 key Funnel mindset hooks  
- 2–3 Tone red flags  

**Rules:**  
- Keep summary ≤ 2 pages.  
- Do not overwrite; always append a new dated section.  

---

### Step 7 — Persist Outputs
Save the **full detailed research deliverable** into the outputs folder.

**Path:**  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md

**File must include:**  
- Full Motivation Map  
- Objection Matrix  
- Brand Audience Framework  
- Funnel Mindset Map  
- Tone Risk Map  
- Complete references and contextual notes  

Do **not** prune down details in this file — it should capture the **entire depth** of Prompt 3’s work.

- Before saving, validate that the header contains:
  - **Date:** {{RUN_DATE}}
  - **Brand:** {{BRAND_NAME}}
- If not, correct automatically.

---

## MCPs
- **Firecrawl** → scrape brand site (science, testimonials, FAQs)  
- **Perplexity** → synthesize objections, triggers, catalysts from forums, Reddit, Quora, industry discussions  
- **Apify (Optional)** → pull marketplace/review/social feeds when product/category is **review-heavy** (e.g., Amazon, Trustpilot, Judge.me, YouTube comments)  

> **Rule of Thumb:** Use Apify only if the category is **marketplace/review/social heavy**. Otherwise, rely on Firecrawl + Perplexity for faster, cheaper runs.  

---

## Deliverables
1. Purchase Motivation Map (per segment)  
2. Objection Matrix (5–7 prioritized objections)  
3. Brand Audience Framework (WHO, Identity, Wish, Relationship, etc.)  
4. Funnel Mindset Map (Top/Mid/Bottom of funnel)  
5. Brand Tone Risk Map  
6. Summarization appended to `brand_context.md`  
7. Full detailed output file saved to:  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md