# Prompt 3 — Purchase Motivation, Objections & Brand Framework

## Inputs

**Required references before proceeding:**

- **Prompt 1 full output:**  
  `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md`

- **Prompt 2 full output:**  
  `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_competitive_landscape_output.md`

- **Consolidated summary context:**  
  `/docs/brand_context.md`

**Critical Usage Rule:**  
- Do **not** proceed unless BOTH full outputs of Prompts 1 and 2 are available.  
- Use `brand_context.md` only as a **summary lens**, never as a substitute for Prompts 1 and 2.  
- If any inputs are missing, stop and request clarifications.

---

## Research Objective

Translate customer psychology (Prompt 1) and competitive landscape (Prompt 2) into a **usable brand framework**.  
Define emotional + logical purchase drivers, identify resistance points, and shape messaging that meets buyers with empathy, proof, and authority.

---

## Steps

### Step 1 — Motivation Map
For each segment (**Strangers, Audience Members, Customers**), provide at least **5–7 motivators**:

- **Emotional motivators** (fear, relief, pride, guilt, hope)  
- **Logical motivators** (ingredients, guarantees, ease-of-use, social proof)  
- **Transformation Promise:** what outcome they *believe* they are buying  
- **Crisis/Catalyst:** tipping moments that move them from consideration → action  

**Requirements:**  
- Ground motivators in **verbatim or near-verbatim language** from Prompt 1 (VoC).  
- Cross-reference competitor themes from Prompt 2.  
- Mark source attribution: `[Prompt 1]`, `[Prompt 2]`, `[CSV Reviews]`, `[External]`.  
- If a motivator feels generic, run an additional Perplexity query and expand before moving on.  

---

### Step 2 — Objection Matrix
Identify at least **5–7 dominant objections**. Present in **table format** with columns:

| Objection (Customer’s words) | Emotional Root | Logical Surface Reason | Strategic Response (copy/proof/offer) | Source |

**Rules:**  
- Emotional root must tie to VoC data (fear of being duped, overwhelm, shame, etc.).  
- Strategic responses must be practical and **ready for copywriting use** (not abstract).  
- Cite source `[Prompt 1]`, `[Prompt 2]`, `[CSV Reviews]`, `[External]`.  
- Thin/vague objections must be re-expanded before finalization.  

---

### Step 3 — Brand Audience Framework
Answer with precision and emotional clarity:

- **WHO** – who is this for? (specific context, not generic)  
- **IDENTITY** – labels/roles customers assign themselves  
- **SECRET WISH** – the unspoken desire they want fulfilled  
- **RELATIONSHIP** – how should they feel about {{BRAND_NAME}}? (guide, friend, protector, expert, rebel, etc.)  
- **POINT OF DIFFERENCE** – unique stance that sets the brand apart  
- **VOICE** – 5 traits (e.g., warm, precise, empowering, irreverent)  
- **PROBLEM** – core emotional + practical problem solved  
- **AWARENESS** – life moment that surfaces the problem  
- **TRANSFORMATION** – change they will feel after success with {{BRAND_NAME}}  

**Requirements:**  
- Each field must reference both **customer language (Prompt 1)** and **competitor positioning (Prompt 2)**.  
- If any field feels thin, expand with additional Perplexity synthesis.  

---

### Step 4 — Funnel Mindset Map
Map beliefs, fears, and trust triggers at each stage. Provide **3–5 insights per stage**:

**Top of Funnel (Strangers):**  
- Beliefs/misunderstandings  
- Fears/avoidances  
- What they’re open to hearing  

**Middle of Funnel (Audience Members):**  
- Internal wrestling/conflicts  
- Key questions they ask  
- What builds trust / what breaks trust  

**Bottom of Funnel (Customers & Post-Purchase):**  
- What they hope will happen  
- Lingering doubts  
- Messages that convert them into advocates  

**Requirements:**  
- Tie each stage back to motivators/objections already mapped.  
- Must include specific **phrases or paraphrases from Prompt 1 + Prompt 2**.  

---

### Step 5 — Brand Tone Risk Map
List **3–5 tonal red flags to avoid**.  

Each red flag must:  
- Be directly tied to an objection or emotional driver (e.g., if fear = shame, avoid “preachy” tone).  
- Include why it creates risk and how to avoid it.  

---

### Step 6 — Summarization → `brand_context.md` (Append/Update)
After completing all steps, **append** a concise section to `/docs/brand_context.md`:

**Title:**  
[Prompt 3] Motivation, Objections & Framework — {{YYYY-MM-DD}}

**Include:**  
- 5–7 core motivators (emotional + logical)  
- Top objections + response themes  
- Brand Framework (Promise, Proof, Personality, Principles)  
- 3 key Funnel mindset hooks  
- 2–3 Tone red flags  

**Rules:**  
- Summary must be ≤ 2 pages.  
- Do not overwrite past context — always append with date.  

---

### Step 7 — Persist Outputs
Save the **full detailed research deliverable** into:

`/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md`

File must include:  
- Full Motivation Map  
- Objection Matrix  
- Brand Audience Framework  
- Funnel Mindset Map  
- Tone Risk Map  
- Complete references + contextual notes  

**Important:** Do **not** prune details. This file must capture the full depth.  

---

## MCPs
- **Firecrawl** → scrape brand site (science, testimonials, FAQs)  
- **Perplexity** → expand motivators, objections, catalysts from forums, Reddit, Quora, industry discussions  
- **Apify (optional)** → scrape marketplaces/review/social feeds (Amazon, Trustpilot, Judge.me, YouTube, TikTok, etc.) when category is **review/social heavy**  

> **Rule of Thumb:** Use Apify only if product category is marketplace/review/social heavy. Otherwise, rely on Firecrawl + Perplexity for speed + cost.  

---

### Step 8 - Iteration Clause (Critical)
After completing each step:  

1. **Review depth**: If any section has fewer than the required details (sentences, examples, proof points), expand automatically.  
2. **Cross-check**: Ensure every step cites inputs from **all required prior prompts**. If not, revise.  
3. **Loop**: Continue refining and expanding until all sections are comprehensive, clear, and evidence-backed.  
4. **No premature finalization**: Do not move forward to summarization or save outputs until quality standards are met.  


---

## Deliverables
1. Motivation Map (≥5–7 motivators per segment)  
2. Objection Matrix (≥5–7 objections, tabular format)  
3. Brand Audience Framework  
4. Funnel Mindset Map (≥3–5 insights per funnel stage)  
5. Tone Risk Map (≥3 red flags)  
6. Summarization appended to `brand_context.md`  
7. Full detailed output saved to:  
   `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/03_purchase_motivation_framework_output.md`