# Prompt 1: Deep Customer & Voice Research (MCP-Enhanced + CSV Reviews)

## Instruction for Cursor
This workflow uses **Firecrawl**, **Tavily**, and **Perplexity** MCP servers.  
Always route crawling and searching through MCPs.  
Your role: act as a **market research strategist + voice-of-customer analyst**, not just a summarizer.  

---

### MCP Integration & Escalation (Required)

- Route all crawling to **Firecrawl** first.
- If a target URL returns **empty/partial** content or appears **JS-rendered**, retry via **Apify**; if still partial, **escalate to Browserbase** and capture:
  - rendered text,
  - first-screen screenshot,
  - URL + timestamp (tag `[Browserbase Capture]`).
- For **VoC depth**, include:
  - **CSV reviews** `[Customer Reviews CSV]` (primary),
  - **Reddit** (if enabled) `[Reddit]`,
  - **YouTube transcripts** (if enabled) `[YouTube]`,
  - Marketplace reviews via **Apify** `[Apify]`.
- Use **Perplexity** for synthesis with **citations** and **Tavily/SerpAPI/Brave** for long-tail discovery.
- Maintain a running **Evidence Ledger** (citations/quotes/tool runs) and save to `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/raw/`.

---

## Step 1: Brand Context (Canonical Sources)
- Pull crawl/search seeds from **`brand_sources.md`**.  
- Use them as the starting dataset; **do not ask the user for URLs**.  
- If any sources are missing, still continue and explicitly flag them in the final report.  

---

## Step 2: Research Objective
Produce a **comprehensive, emotionally detailed portrait of the customer landscape** for **[Brand Name]**.  

**Goals:**
- Reveal **core psychological drivers** behind why people do or don’t buy.  
- Capture **authentic voice-of-customer (VoC)** across brand-owned, category-wide, and review data.  
- Build **3 complete Ideal Customer Personas (ICPs)** with *layered emotions, identity conflicts, and moment-of-need triggers*.  
- Provide a **marketing-usable dataset** (quotes, metaphors, unmet needs, tensions).  

---

## Step 3: Audience Segments
Develop 3 distinct ICPs:  
1. **Strangers** — unaware of brand/problem.  
2. **Audience Members** — aware of brand/problem but not yet purchased.  
3. **Customers** — existing/past buyers.  

---

## Step 4: Data Gathering (MCP + CSV)
- **Firecrawl** → Crawl brand-owned assets (site, product, mission, blog). Extract claims, emotional framing, tone.  
- **Tavily** → Search external coverage (press, blogs, Quora, parenting forums, reviews outside owned sites). Extract broad cultural/category sentiment.  
- **Perplexity** → Gather user-generated chatter (Reddit, TikTok, Instagram, Amazon reviews). Highlight figurative/identity-driven language.  

**If CSV file at `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv`:**
- Parse review text + rating + author + source.  
- Treat this as the **primary Voice of Customer dataset**.  
- Rank recurring phrases by **frequency × emotional intensity**.  
- Mark them as **[Customer Reviews CSV]** in outputs.  

---

## Step 4B: Voice-of-Customer Enrichment (Qualitative)

- Extract **20–30 recurring phrases** with **frequency × emotional intensity**.  
- Pull **6+ Reddit quotes** and **2+ YouTube transcript excerpts** (if those MCPs are enabled).  
- Mark **identity conflicts**, **metaphors**, and explicit **shame/guilt/fear language**.  
- Add a **Narrative Persona subsection** for each ICP — one tight paragraph *written in their voice* using verbatim snippets.  
- If quotas are not met, **auto-iterate additional queries** such as:  
  - “regret after purchase {{category}}”  
  - “is it worth it {{brand}} review”  
  - “return policy {{brand}}”  
  - “durability {{product}}”  

---

## Step 5: Persona Construction Requirements
For each ICP, provide:

### Demographics & Identity
- Age, gender, income, household  
- Parenting/decision-making roles  
- Values, lifestyle, identity labels  

### Emotional Drivers
- Persistent frustrations, unmet needs  
- Core fears, guilt, shame, anxieties  
- Deep aspirations, desired transformations  
- Identity conflicts (e.g., *“I want to be a creative parent, but I fear the mess/cost”*)  
- Emotional cost of inaction  

### Awareness & Triggers
- Seasonal, situational, emotional triggers  
- Phrases/language used when problem crystallizes  
- Behavioral signals that show readiness to act  

### Voice of Customer Insights
- Extract **20–30 recurring phrases or quotes** across CSV + web.  
- Rank by **frequency + emotional intensity**.  
- Group into **themes** (hope, confusion, guilt, pride, urgency, delight).  
- Highlight **metaphors & figurative language** (e.g., *“a lifesaver,” “our living room turned into a spaceship”*).  
- Explicitly separate:  
  - [Customer Reviews CSV]  
  - [External Web Sources]  

---

## Step 6: Synthesis Requirements
- **Compare segments** (what Strangers fear vs what Customers celebrate).  
- **Highlight contradictions** (e.g., “too expensive” vs “worth every penny”).  
- **Identify unmet needs** (requests, complaints, gaps).  
- **Strategic implications** — what messaging hooks, features, or campaigns flow directly from these tensions.  

---

## Step 6B: Evidence Quotas & Iterate
- Do not finalize until **ALL** apply:
  - `CITATIONS >= MIN_CITATIONS`
  - `DIRECT_QUOTES >= MIN_DIRECT_QUOTES`
  - If Reddit/YouTube are available: `REDDIT_QUOTES >= MIN_REDDIT_QUOTES` and `YT_TRANSCRIPTS >= MIN_YT_TRANSCRIPTS`
  - Prompt 2 only: `COMPETITORS >= MIN_COMPETITORS`
- If any quota is unmet, **generate targeted follow-up queries** and repeat retrieval/synthesis up to `MAX_ITERATIONS` or until quotas pass.
- Log remaining gaps in a **[LIMITATIONS]** section with next best queries to run.

---

### Step 7: Iteration Clause (Critical)
After completing each step:  

1. **Review depth**: If any section has fewer than the required details (sentences, examples, proof points), expand automatically.  
2. **Cross-check**: Ensure every step cites inputs from **all required prior prompts**. If not, revise.  
3. **Loop**: Continue refining and expanding until all sections are comprehensive, clear, and evidence-backed.  
4. **No premature finalization**: Do not move forward to summarization or save outputs until quality standards are met.  

---

## Step 8: Deliverables
1. **Three Full ICP Profiles** (Strangers, Audience, Customers).  
2. **Top 20–30 VoC Phrases** (ranked + themed, with source tags).  
3. **Emotional Theme Map** — fears, motivators, unmet needs.  
4. **Metaphors & Identity Conflicts** — explicit bullet list.  
5. **Emergent Tensions & Strategic Implications**.  
6. **Missing Source Note** (if any gaps in brand_sources.md).  

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

## Step 9: Append to `brand_context.md`
After full report is done, create a **concise ≤2 page summary** and append to `brand_context.md`.  

### Format:
```markdown
[Prompt 1] Customer & Voice Summary — YYYY-MM-DD

Brand Overview: <1–3 lines>

Audience Snapshots:
Strangers: <1 sentence>  
Audience Members: <1 sentence>  
Customers: <1 sentence>  

Key Emotional Drivers:
- Motivator 1
- Motivator 2
- Fear 1
- Fear 2

Top 5 VoC Phrases:
"<phrase>" — [Customer Reviews CSV]  
"<phrase>" — [External Web Sources]  

Metaphors / Conflicts:
- <bullet point>  

Strategic Watchouts:
- <bullet point>  

Sources Used:
- [CSV reviews]  
- [brand_sources.md]  
- [External Web Sources]


## Step 10: Persist Outputs
After completing Step 8, persist the **full research output** to the `/outputs/` directory.

### Instructions

1. **Create Brand Folder**
   - Inside `/outputs/`, check if the folder `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/` exists.  
   - If it does **not** exist, create it.  
   - This folder will serve as the single container for all outputs generated for that brand and date.

2. **Save Full Report**
   - Write the complete deliverable for Prompt 1 (all ICP profiles, VoC lists, emotional drivers, metaphors, identity conflicts, emergent tensions, and source notes) to:  
     ```
     /outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md
     ```

3. **Append Summary**
   - Append the concise summary block (from Step 8) into:  
     ```
     /docs/brand_context.md
     ```
   - Do not overwrite previous sections. Always append as a new dated section.

4. **Source Traceability**
   - In the full output file, include the **complete list of references and sources** with contextual notes.  
   - Do not update `brand_sources.md` directly; it remains the canonical seed list for crawling.

---

✅ **Note:**  
- Before saving, validate that the header contains:
  - **Date:** {{RUN_DATE}}  
  - **Brand:** {{BRAND_NAME}}  
- If not, correct automatically.  

Future prompts will also save their full outputs into the **same `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/` folder**, following this standardized naming convention.