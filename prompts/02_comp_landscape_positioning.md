# Prompt 2 — Competitive Landscape & Positioning

## Instruction for Cursor
Use **Tavily**, **Firecrawl**, **Perplexity** MCP servers.  
Optionally use **Apify** when marketplaces/reviews/social feeds require deeper scraping than Firecrawl.  
Do **not** ask the user for URLs; read all seeds from `brand_sources.md`.  
All insights must be evaluated through the customer truths in `brand_context.md` (Prompt 1 outputs).

---

### Report Header Standard
- Always use **RUN_DATE** and **BRAND_NAME** provided by the workflow.
- If RUN_DATE is not explicitly passed, parse it from the output folder path `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`.
- Never take the date or brand name from examples, sources, or defaults.

The report header must always begin:

**Date:** {{RUN_DATE}}  
**Brand:** {{BRAND_NAME}}

---

## Step 1 — Brand Context (Centralized Sources)
- Read crawl/search seeds from **`brand_sources.md`** (competitor leads may be listed here too).
- Read the latest **customer/VoC/emotional drivers** from both:
  - The **summary** in `/docs/brand_context.md` (Prompt 1 appended block).
  - The **full raw output** from:
    ```
    /outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/01_deep_customer_voice_research_output.md
    ```
- Use the summary for alignment/lens consistency, and the full report for detailed depth.  
- If specific competitor seeds are missing, proceed with discovery and note gaps in the final output.

---

## Step 2 — Competitor Discovery (Tavily)
- Identify:
  - **3–5 direct competitors** (similar product/solution).
  - **2–3 indirect competitors** (serve the same emotional/job-to-be-done via different solutions).
- Prioritize brands with strong visibility in **search, socials, or marketplaces**.

---

## Step 3 — Source Collection (Firecrawl + Optional Apify)
For each selected competitor, gather sources:

- **Firecrawl**:  
  - Homepage / hero landing  
  - Best-seller PDP (or main offer page)  
  - About/Mission page  
  - Blog/Education hub  
  - Public social links (from the site footer/header)

- **Optional: Apify** (use only if needed; otherwise skip to reduce latency/cost):  
  - Marketplaces (e.g., **Amazon** product pages + reviews)  
  - Review platforms (e.g., **Trustpilot**, **Judge.me**)  
  - Social feeds where Firecrawl is insufficient (Instagram/TikTok/YouTube post text, bios)  

  > **Usage Rule of Thumb:** Keep Apify optional. Use it only when the category is **marketplace/review/social heavy** and Firecrawl cannot provide sufficient depth. For most categories, **Firecrawl + Tavily + Perplexity** is faster and cheaper while still delivering strategic richness.

> Save raw extracts (titles, H1/H2, hero copy, PDP bullets, review snippets). Prefer verbatim copy for message analysis.

---

## Step 4 — Customer Lens Integration (Truth Filter)
- From **`brand_context.md` Prompt 1**: load  
  - Top VoC phrases,  
  - Emotional drivers (motivators + fears),  
  - Awareness triggers,  
  - Identity conflicts/metaphors.  
- Treat these as the **evaluation lens** for all competitive claims (alignment vs. mismatch).

---

## Step 5 — Feature & Message Analysis (per competitor)
Document the following, using extracted/quoted copy where possible:

- **Core Features** (what they emphasize)  
- **Benefits & Solutions** (problems framed as solved)  
- **Outcomes Promised** (life/identity change)  
- **Emotional Angles** (fears, desires, identity hooks)  
- **Offer Structure** (discounts, bundles, guarantees, trials, subscriptions)  
- **CTA Style** (urgency, empowerment, ease, FOMO)  
- **Messaging Language** (headlines, taglines, positioning lines)  
- **Customer Echoes** (where the copy mirrors or contradicts Prompt 1 VoC)

> Note explicit **price anchors** if visible (one-time price, bundle price, subscription cadence).

---

## Step 6 — Visual & Tonal Audit (per competitor)
From site/socials:

- **Visual Identity**: palette, type, imagery/photography style, layout density  
- **Design Signals**: luxury, science/clinical, warmth, simplicity, urgency, playfulness  
- **Tone of Voice**: clinical vs. empathetic, premium vs. casual, bold vs. careful  
- **Consistency Check**: do visuals & tone support or undermine the written claims?  
- **Customer Alignment**: compare to emotional drivers in `brand_context.md`

---

## Step 7 — Positioning Comparison Table
Create a structured comparison across competitors:

| Competitor | Key Promise / Positioning | Proof Devices | Features | Benefits | Emotional Angles | Offer Mechanics | Visual Identity | Voice & Tone | Outcome Promised | Price Anchor (if visible) |

> Keep cells concise but specific; prefer short, sourced phrases over paraphrase.

---

## Step 8 — SWOT & Differentiation Map for {{BRAND_NAME}}
Grounded in Steps 4–7:

- **SWOT**  
  - **Strengths**: where {{BRAND_NAME}} naturally aligns with VoC truths (from Prompt 1)  
  - **Weaknesses**: internal message/product gaps vs. competitors  
  - **Opportunities**: category **white space** (benefits/emotions customers want but competitors underplay)  
  - **Threats**: saturated claims, misaligned category norms, trust barriers

- **Differentiation Map** (rank 3–5)  
  - **Messaging White Space** (emotional/functional)  
  - **Emotional Mismatches** (competitor claims vs. real VoC pain/desire)  
  - **Audience Blind Spots** (ignored segments/identity cues)  
  - **Overused Tropes** (fatigued, manipulative phrases)  
  - **Narrative/Visual Gaps** (stories/tones/designs customers crave but don’t see)

---

## Deliverables
1. **Competitor Profiles** (3–5, each with Steps 5–6 distilled).  
2. **Positioning Comparison Table** (Step 7).  
3. **Ranked Messaging & Emotional Patterns** (what dominates the space vs. what’s missing).  
4. **SWOT** for {{BRAND_NAME}}.  
5. **Differentiation Map** (top 3–5 opportunities with rationale).

---

## Guidelines
- Use **sourced, verbatim** language wherever possible; minimize paraphrase.  
- Evaluate every claim through the **Prompt 1 VoC/emotional lens**.  
- Call out **price anchors** and **offer mechanics** explicitly (they drive positioning).  
- Prefer bullets, tables, and ranked lists over long prose.

---

## Step 9 — Summarization → `brand_context.md` (Append/Update)
After completing all deliverables, **append** a concise, dated summary to **`brand_context.md`** under a new section.

- Keep the appended block **≤ 1–2 pages**.  
- Do **not** overwrite previous sections; always append a new dated section.  

### Format to Append
```markdown
[Prompt 2] Competitive Landscape Summary — YYYY-MM-DD

Category Snapshot (10–15 lines):
- <what most competitors emphasize; norms, repeated promises, common proof devices>

Top Messaging/Emotional Patterns (ranked):
1) <theme> — why it dominates
2) <theme> — why it dominates
3) <theme> — why it dominates

Positioning Comparison (compact highlights):
- <Competitor A: key promise / price anchor / offer mechanic>
- <Competitor B: ...>
- <Competitor C: ...>

SWOT for {{BRAND_NAME}} (succinct):
- Strengths: <bullets>
- Weaknesses: <bullets>
- Opportunities: <bullets>
- Threats: <bullets>

Differentiation Opportunities (ranked 3–5):
1) <opportunity> — (VoC alignment + competitor gap)
2) <opportunity> — (...)
3) <opportunity> — (...)

Sources Used:
<compact list of domains/handles; full list remains in brand_sources.md>

## Step 10 — Persist Outputs

After completing the summarization in Step 9, persist the **full research output** to the `/outputs/` directory.

- Before saving, validate that the header contains:
  - **Date:** {{RUN_DATE}}
  - **Brand:** {{BRAND_NAME}}
- If not, correct automatically.

### Instructions

1. **Reuse Brand Folder**
   - Navigate to `/outputs/` and check for the folder:
     ```
     /outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/
     ```
   - If the folder does not exist (e.g., Prompt 1 has not been run), create it.
   - All Prompt 2 outputs must be stored in this same folder to keep the brand/date deliverables centralized.

2. **Save Full Report**
   - Write the **complete deliverable for Prompt 2** — including competitor profiles, positioning comparison table, messaging/emotional pattern analysis, SWOT, differentiation map, and references — to:
     ```
     /outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/02_competitive_landscape_output.md
     ```

3. **Source Traceability**
   - In the full output file, include the **complete list of references and sources** with contextual notes (e.g., why each source was used).
   - Do **not** update `brand_sources.md` directly. It remains the canonical seed list for crawling and discovery.

---

✅ **Note:** This ensures Prompt 2’s complete output is saved alongside Prompt 1’s deliverables, using a consistent folder and filename convention:

