# usage_instructions.md
**How to Run the Brand Brief Generator (for any brand)**

---

## 0) Prerequisites

- Install **Cursor Desktop**.
- In **Cursor → Settings → Model Context Protocol (MCP)**, ensure these servers are **green** (API keys required):
  - **firecrawl-mcp** — scrapes brand sites (home, PDPs, FAQs, blog).  
    Required: `FIRECRAWL_API_KEY`
  - **perplexity-mcp** — synthesizes/expands insights from forums, Reddit, Quora, open web.  
    Required: `PERPLEXITY_API_KEY`
  - **tavily-remote-mcp** — targeted web queries for competitor/discovery support.  
    Required: `TAVILY_API_KEY`
  - **apify (optional)** — marketplace/review/social scraping (Amazon, Trustpilot, YouTube, TikTok, IG).  
    Use only for review/social-heavy categories.
- Ensure these folders exist (create if needed):
  - Data (optional reviews CSV):  
    ```
    /data/brand_reviews/
    ```
  - Outputs destination:  
    ```
    /outputs/
    ```

---

## 1) Add Brand Sources (the seeds)

Open:
/docs/brand_sources.md

Fill every structured field:

- Brand Name
- Geography
- Category
- Website
- Product Detail Pages (PDPs)
- About/Mission
- Blog/Education
- Socials
- Press/Owned Media
- Marketplaces
- Review Platforms
- Competitor Leads (optional)

> **Important:** The **Brand Name** value is used as `{{BRAND_NAME}}` across the workflow. Keep it consistent and free of extra spaces.

---

## 2) (Optional) Add Customer Reviews

If you have reviews, save a CSV here:
/data/brand_reviews/{{BRAND_NAME}}_reviews.csv

**Required headers (exactly):**
review_text, rating, source, author, product, date

Rules:
- If present, the CSV is treated as the **primary Voice of Customer** dataset and is tagged **[Customer Reviews CSV]**.
- If missing, the system falls back to MCP crawling/discovery; web-sourced insights are tagged **[External Web Sources]**.

---

## 3) Verify Outputs Folder

Ensure the outputs folder exists (it can be empty before first run):
/outputs/

---

## 4) Run the Workflow

Open:
/prompts/00_master_workflow.md

### ⚙️ Model Selection

Before running, select the model in Cursor:

- **GPT-5** → Recommended for best balance of depth, creativity, and speed.  
- **Auto** → Cursor automatically selects the most reliable model (safer if you’re unsure).  
- **Max Mode** → Only needed when your context (sources + CSV + prior outputs) exceeds ~200k tokens.  
  ⚠️ Slower and more expensive — use only for very large datasets.

If you skip this step, Cursor may default to a lighter model, which can cause thinner, less VoC-rich outputs.

Then run in Cursor:
/run 00_master_workflow.md

The workflow will:
1. Check for `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` (optional).
2. Execute **Prompts 01 → 04** in sequence.
3. Save full, detailed outputs to:
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/

4. Append concise summaries (≤2 pages per prompt) to:
/docs/brand_context.md

**Mandatory input rule (prompts will halt if unmet):**
- **Prompt 2** requires Prompt 1 full output **and** `brand_context.md`.
- **Prompt 3** requires Prompt 1 & 2 full outputs **and** `brand_context.md`.
- **Prompt 4** requires Prompt 1, 2 & 3 full outputs **and** `brand_context.md`.

---

## 5) Read Results

- **Quick overview (summaries):**
/docs/brand_context.md

- Each prompt appends a **dated** summary section (≤2 pages).  
- Summaries are **appended**—never overwritten.

- **Full detailed outputs (by prompt):**
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/

Files created:
- `01_deep_customer_voice_research_output.md`
- `02_competitive_landscape_output.md`
- `03_purchase_motivation_framework_output.md`
- `04_messaging_funnel_strategy_output.md`

---

## 6) Run for Another Brand

1. Update `/docs/brand_sources.md` with the new brand.
2. (Optional) Add `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv`.
3. Re-run:
/run 00_master_workflow.md

A new dated folder is created automatically under `/outputs/`.

---

## 7) Troubleshooting

- **MCP server is red** → Check API keys and server paths in Cursor **Settings → MCP**.
- **No outputs saved** → Confirm `/outputs` exists and `Brand Name` in `brand_sources.md` matches your file names (no trailing spaces).
- **CSV ignored** → File name must be exactly `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` and include the required headers.
- **Prompt halts** → One or more required inputs (prior full outputs or `brand_context.md`) are missing. Generate them, then re-run.
- **Summaries look thin** → Summaries are capped at ~2 pages by design. Open the full prompt outputs in `/outputs/` for complete detail.
- **Runs feel short/generic** → Ensure you’re using the updated prompts that include the **Iteration Clause**; verify MCP servers are green and `brand_sources.md` is fully populated.
- **Runs loop/expand repeatedly** → The **Iteration Clause** is self-expanding. Check for sparse sources, missing competitor seeds, or malformed CSV headers causing limited evidence.

---

## 8) Notes

- Prompts **2–4** require the **full detailed outputs** of earlier prompts **plus** `brand_context.md`.
- Each prompt appends a new dated summary to `brand_context.md` (**never overwrite**).
- **Iteration Clause** is included across prompts to self-expand until outputs are **comprehensive and evidence-backed**.
- **apify** is optional and used only for **review/social-heavy** categories.
- All deliverables follow the `01–04` file naming convention in `/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/`.

---

# quickstart.md
**Brand Brief Generator — Quickstart Checklist**

---

## ✅ Preflight

- [ ] Cursor Desktop installed  
- [ ] MCP servers **green** in Settings → MCP  
  - [ ] firecrawl-mcp (`FIRECRAWL_API_KEY`)  
  - [ ] perplexity-mcp (`PERPLEXITY_API_KEY`)  
  - [ ] tavily-remote-mcp (`TAVILY_API_KEY`)  
  - [ ] apify (optional; only for review/social-heavy)  
- [ ] Folders exist:
  - [ ] `/data/brand_reviews/`
  - [ ] `/outputs/`

---

## 🧭 Configure Sources

- [ ] Filled **all fields** in `/docs/brand_sources.md`  
- [ ] (Optional) Placed CSV at `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` with headers:  
      `review_text, rating, source, author, product, date`

---

## ▶️ Run

- [ ] Open `/docs/00_master_workflow.md`  
- [ ] Run:
/run 00_master_workflow.md

css
Copy
Edit
- [ ] Confirm it creates:
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/

---

## 🔎 Find Outputs

- [ ] Summaries (≤2 pages each): `/docs/brand_context.md`  
- [ ] Full detail per prompt:
- [ ] `01_deep_customer_voice_research_output.md`
- [ ] `02_competitive_landscape_output.md`
- [ ] `03_purchase_motivation_framework_output.md`
- [ ] `04_messaging_funnel_strategy_output.md`

---

## 🧩 Dependencies (will halt if missing)

- [ ] Prompt 2 requires Prompt 1 full output + `brand_context.md`
- [ ] Prompt 3 requires Prompt 1 & 2 full outputs + `brand_context.md`
- [ ] Prompt 4 requires Prompt 1, 2 & 3 full outputs + `brand_context.md`

---

## 🛠 Troubleshooting

- [ ] MCP red? Fix API keys/paths.  
- [ ] No files? Check `/outputs/` exists and Brand Name consistency.  
- [ ] CSV ignored? Verify exact file name + headers.  
- [ ] Output too thin? Ensure updated prompts with **Iteration Clause** + complete sources.  
- [ ] Output loops? Likely sparse evidence—add sources/competitors or CSV.

---