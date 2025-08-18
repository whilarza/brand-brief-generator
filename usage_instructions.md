**How to Run the Brand Brief Generator (for any brand)**

0) Prerequisites
----------------

*   Install **Cursor Desktop**.
    
*   Confirm **MCP servers** in Cursor → Settings → _Model Context Protocol (MCP)_ are **green**:
    
    *   firecrawl-mcp (requires FIRECRAWL\_API\_KEY)
        
    *   tavily-remote-mcp (requires TAVILY\_API\_KEY)
        
    *   perplexity-mcp (requires PERPLEXITY\_API\_KEY)
        
    *   _(Optional)_ apify for marketplace/social-heavy brands
        
*   /docs/prompts/outputs/data/brand\_reviews
    

1) Add brand sources (the seeds)
--------------------------------

Open /docs/brand_sources.md and fill in the structured fields:

*   Brand Name
    
*   Geography
    
*   Category
    
*   Website
    
*   Product Detail Pages (PDPs)
    
*   About/Mission
    
*   Blog/Education
    
*   Socials
    
*   Press/Owned Media
    
*   Marketplaces
    
*   Review Platforms
    
*   Competitor Leads (optional)
    

> **Important:** The Brand Name field is what the workflow uses as {{BRAND\_NAME}}.

2) (Optional) Add customer reviews
----------------------------------

If you have reviews, save them as a CSV file in:

/data/brand_reviews/{{BRAND_NAME}}_reviews.csv

The file must include headers:

review_text, rating, source, author, product, date   `

*   If the CSV is present, it is treated as the **primary source of VoC**.
    
*   If missing, the workflow falls back to scraping and web discovery.
    

3) Verify outputs folder
------------------------

Make sure /outputs exists. It can be empty.

4) Run the workflow
-------------------

In Cursor, open 00_master_workflow.md and run:

/run 00_master_workflow.md

The workflow will:

1.  Check for a reviews CSV.
    
2.  Execute Prompts 01 → 04 in sequence.
    
3.  /outputs/{{YYYY-MM-DD}}\_{{BRAND\_NAME}}/
    
4.  /docs/brand\_context.md
    

5) Read results
---------------

*   **Quick overview:** /docs/brand\_context.md
    
*   **Detailed outputs:** /outputs/{{YYYY-MM-DD}}\_{{BRAND\_NAME}}/
    

6) Run for another brand
------------------------

1.  Update /docs/brand\_sources.md with the new brand.
    
2.  (Optional) Add /data/brand\_reviews/{{BRAND\_NAME}}\_reviews.csv.
    
3.  /run 00\_master\_workflow.md
    

A new dated folder will be created automatically under /outputs/.

7) Troubleshooting
------------------

*   **MCP server is red** → Check API keys or server path in Cursor settings.
    
*   **No outputs saved** → Confirm /outputs exists and that Brand Name in brand\_sources.md has no extra spaces.
    
*   **CSV ignored** → File name must exactly match /data/brand\_reviews/{{BRAND\_NAME}}\_reviews.csv and include the required headers.
    
*   **Errors mid-run** → Cursor will show which step failed. Fix the issue, then re-run that prompt or the whole workflow.
    
*   **Summaries too long** → They are auto-truncated to ~2 pages in brand\_context.md. Full details are always in /outputs/.
    

8) Notes
--------

*   Prompts 2–4 always reference the **full detailed output** of earlier prompts.
    
*   apify is invoked only when review/social/marketplace scraping is critical.
    
*   CSV-sourced VoC insights are tagged **\[Customer Reviews CSV\]**; web-sourced insights are tagged **\[External Web Sources\]**.