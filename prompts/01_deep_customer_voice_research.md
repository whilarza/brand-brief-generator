# Prompt 1: Deep Customer & Voice Research (MCP-Enhanced + CSV Reviews)

## Instruction for Cursor
This workflow uses **Firecrawl**, **Tavily**, and **Perplexity** MCP servers.  
Always route crawling and searching through MCPs.  
Your role: act as a **market research strategist + voice-of-customer analyst**, not just a summarizer.  

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