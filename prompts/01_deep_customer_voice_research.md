# Prompt 1: Deep Customer & Voice Research (MCP-Enhanced + CSV Reviews)

## Instruction for Cursor
This workflow uses **Firecrawl**, **Tavily**, and **Perplexity** MCP servers.  
When asked to crawl or search, route those requests through the MCPs instead of default search.  
Combine results into structured, psychologically rich outputs as described.

---

### Report Header Standard
- Always use **RUN_DATE** and **BRAND_NAME** provided by the workflow.
- If RUN_DATE is not explicitly passed, parse it from the output folder path `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`.
- Never take the date or brand name from examples, sources, or defaults.

The report header must always begin:

**Date:** {{RUN_DATE}}  
**Brand:** {{BRAND_NAME}}

---

## Step 1: Brand Context (Centralized Sources)
Read crawl/search seeds from **`brand_sources.md`** (do not prompt the user for URLs).  
If any required section is empty in `brand_sources.md`, proceed with available sources and note missing items in the final Deliverables.

---

## Step 2: Research Objective
Conduct in-depth customer research to build emotionally grounded, segment-specific **Ideal Customer Personas (ICPs)** for **[Brand Name]**.

**Focus**
- Uncover real customer fears, motivations, metaphors, identity conflicts, and moment-of-need triggers.  
- Use only publicly available language and sentiment data.  
- Deliver detail suitable for brand strategy and messaging development.

---

## Step 3: Audience Segments
Build one distinct ICP for each:
1. **Strangers** — not yet aware of brand/problem  
2. **Audience Members** — aware but not purchased  
3. **Customers** — already purchased/engaged

---

## Step 4: Data Gathering (MCP Integration + CSV Review File)

Use MCP servers as follows (derive targets from `brand_sources.md`):

- **Firecrawl** → Crawl product pages, blog posts, brand mission, about page. Extract messaging, claims, emotional framing.  
- **Tavily** → Surface broader web sentiment: forums, Quora, press, blogs, third-party discussions. Map category context.  
- **Perplexity** → Mine user-generated content (e.g., Reddit, Amazon, TikTok, Instagram). Group by theme; prioritize high-emotion language.  

**If a CSV file exists at `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv`:**
- Parse the CSV for **review text, rating, author, and source columns**.  
- Treat this as the **primary Voice of Customer dataset**.  
- Rank recurring phrases, emotional expressions, and metaphors by **frequency + emotional intensity**.  
- Label them as **[Customer Reviews CSV]** in the final Sources list.  

---

## Step 5: Persona Construction Requirements
For each ICP, document:

### Demographics & Identity Markers
- Age, gender, income, household  
- Role in decision-making  
- Labels/self-descriptions, lifestyle, values

### Emotional & Psychological Drivers
- Persistent worries, frustrations  
- Core fears, guilt, shame  
- Aspirations, desired transformations  
- Identity conflicts (e.g., “I want X, but feel Y”)  
- Emotional consequences of inaction

### Awareness & Trigger Moments
- Situational, seasonal, emotional triggers  
- Language used when realizing the problem  
- Behavioral signals they’re ready to act

### Voice of Customer (VoC) Insights
- Extract **10–15 most repeated phrases**  
- Rank by **frequency + emotional intensity**  
- Include **direct quotes** or close paraphrases with sources  
- Group by theme (confusion, urgency, optimism, disappointment)  
- Highlight **metaphors, figurative language, identity conflicts**  
- Distinguish **pre-purchase vs post-purchase**  
- Clearly separate insights into:
  - [Customer Reviews CSV]  
  - [External Web Sources]  

---

## Step 6: Final Deliverables
- Three ICP Profiles (Strangers, Audience, Customers)  
- Top 15 VoC Phrases (Ranked + Themed)  
- Emotional Theme Summary → fears, motivators, unmet needs  
- Metaphors & Identity Conflicts → explicitly called out  
- Emergent Trends/Tensions → strategic implications  
- **Missing Sources Note** (if any sections in `brand_sources.md` were empty)  

---

## Step 7: Guidelines
- Use only **publicly available, sourced customer language**  
- Do **not fabricate** quotes; paraphrase only recurring patterns  
- Be explicit about **emotional tone + trigger context**  
- Keep structure **clean, exportable, and ready for downstream strategy**

---

## Step 8: Summarization → `brand_context.md` (Append/Update)
After completing all deliverables, **append** a concise summary to `brand_context.md` under a new dated section.

- Keep the appended block **≤ 1–2 pages**  
- If the draft exceeds 2 pages, **truncate to the most representative insights**  
- Do **not** overwrite previous sections; always append a new dated section  

### Format to Append
```markdown
[Prompt 1] Customer & Voice Summary — YYYY-MM-DD

Brand Overview: <1–3 lines: product, promise, positioning>

Audience Segments (Shortform):
Strangers: <one-sentence description>  
Audience Members: <one-sentence description>  
Customers: <one-sentence description>  

Key Emotional Drivers:
- Motivator 1
- Motivator 2
- Motivator 3
- Fear 1
- Fear 2
- Fear 3

Top 5 VoC Phrases (most representative):
"<phrase>" — [Customer Reviews CSV]  
"<phrase>" — [Customer Reviews CSV]  
"<phrase>" — [External Web Sources]  
"<phrase>" — [External Web Sources]  
"<phrase>" — [External Web Sources]  

Metaphors / Identity Conflicts (notable):
- <bullet point>
- <bullet point>

Strategic Watchouts:
- <emergent risks/tensions that affect messaging>

Sources Used:
- [Customer Reviews CSV]  
- [brand_sources.md seeds]  
- [External Web Sources]


## Step 9: Persist Outputs
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

Future prompts will also save their full outputs into the **same `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/` folder**, following this standardized naming convention:

