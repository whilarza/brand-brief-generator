# quickstart.md
**Brand Brief Generator — Quickstart Checklist**

---

## ✅ Preflight

- [ ] Install **Cursor Desktop**  
- [ ] In **Cursor → Settings → MCP**, confirm these are **green**:
  - [ ] `firecrawl-mcp` (requires `FIRECRAWL_API_KEY`)  
  - [ ] `perplexity-mcp` (requires `PERPLEXITY_API_KEY`)  
  - [ ] `tavily-remote-mcp` (requires `TAVILY_API_KEY`)  
  - [ ] `apify` (optional; for social/marketplace scraping)

---

## 🧭 Configure Sources

- [ ] Open `/docs/brand_sources.md` and fill in:  
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

- [ ] (Optional) Place CSV reviews file at:  
/data/brand_reviews/{{BRAND_NAME}}_reviews.csv

**Required headers (exactly):**  
review_text, rating, source, author, product, date

---

## ▶️ Run the Workflow

- [ ] Open:
/docs/00_master_workflow.md

- [ ] Run in Cursor:
/run 00_master_workflow.md

- [ ] Confirm it creates:
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/

---

## 🔎 Review Outputs

- [ ] **Quick summaries (≤2 pages each):**  
/docs/brand_context.md

- [ ] **Full detailed outputs (per prompt):**  
/outputs/{{YYYY-MM-DD}}_{{BRAND_NAME}}/

Files generated:
- `01_deep_customer_voice_research_output.md`  
- `02_competitive_landscape_output.md`  
- `03_purchase_motivation_framework_output.md`  
- `04_messaging_funnel_strategy_output.md`

---

## 🧩 Dependencies (Prompts Will Halt if Missing)

- [ ] Prompt 2 requires: Prompt 1 full output **+** `brand_context.md`  
- [ ] Prompt 3 requires: Prompt 1 & 2 full outputs **+** `brand_context.md`  
- [ ] Prompt 4 requires: Prompt 1, 2 & 3 full outputs **+** `brand_context.md`

---

## 🛠 Troubleshooting

- [ ] **MCP server is red** → Check API keys and paths in Cursor → Settings → MCP  
- [ ] **No outputs saved** → Ensure `/outputs/` exists and `Brand Name` is consistent in file names  
- [ ] **CSV ignored** → File must match `/data/brand_reviews/{{BRAND_NAME}}_reviews.csv` and include exact headers  
- [ ] **Outputs too thin** → Confirm updated prompts include the **Iteration Clause** and that sources are complete  
- [ ] **Infinite expansions** → Add competitor leads or more sources; check CSV formatting  
- [ ] **Summaries differ from full detail** → This is expected. Summaries cap at ~2 pages; open full outputs in `/outputs/` for complete detail.

---