# Query Templates

Reusable research prompts & extraction specs for the Brand Brief Generator.

Use these templates when a prompt says **"use the query templates."**

Replace placeholders like `{{BRAND_NAME}}`, `{{category}}`, `{{competitor}}`, `{{product}}`.

---

## 0) Conventions (read once)

- **Tag sources** in outputs: `[Firecrawl] [Perplexity] [Tavily] [SerpAPI] [Brave] [Apify] [Browserbase] [Reddit] [YouTube] [CSV] [Prompt1] [Prompt2] [Prompt3]`.

- Prefer **verbatim** text for messaging, headlines, reviews, and quotes.

- Use the **Output Schema** exactly where specified so tables/merges stay clean.

- When a result is empty/thin → **retry** via Apify; still thin → **escalate** the exact URL to Browserbase and capture rendered text + screenshot.

---

## 1) Feature & Message Analysis (Competitor)

**When:** Prompt 2, Step 5

**Inputs:** `{{competitor}}`, URLs (home, PDP, about, blog), social handles (optional)

**Query**

> Extract **verbatim** messaging from {{competitor}} across homepage, best-seller PDP, about/mission, and top blog/education page. Identify **Core Features**, **Benefits/Solutions**, **Outcomes Promised**, **Emotional Angles**, **Offer Structure**, **CTA Style**, **Positioning Lines**. Include **price anchors** if visible.

**Output Schema**

```json
{
"competitor": "{{competitor}}",
"features": ["...", "...", "..."],
"benefits": ["...", "..."],
"outcomes_promised": ["...", "..."],
"emotional_angles": ["...", "..."],
"offer_mechanics": ["discount X / bundle Y / guarantee Z / trial N", "..."],
"cta_style": ["urgency", "ease", "empowerment", "..."],
"positioning_lines": ["", ""],
"price_anchors": ["$...", "from $...", "subscription ..."],
"citations": ["url1", "url2", "..."]
}
```

## 2) Visual & Tonal Audit (Competitor)

**When:** Prompt 2, Step 6

**Inputs:** {{competitor}}, same URLs as above

**Query**

Analyze visual identity (palette, typography, imagery), layout density, design signals (luxury, scientific, warm, playful, urgent), and tone of voice (clinical ↔ empathetic; premium ↔ casual; bold ↔ careful). Note consistency between visuals & claims and alignment/mismatch with known VoC drivers in brand_context.md. Use short, specific phrases.

**Output Schema**

```json
{
"competitor": "{{competitor}}",
"visual_palette": ["hex or descriptors", "..."],
"typography": ["serif/sans/mono + vibe"],
"imagery_style": ["studio/UGC/illustration/lifestyle", "..."],
"layout_density": "minimal / dense / modular / editorial",
"design_signals": ["luxury", "science", "warmth", "playful", "urgent", "..."],
"tone_of_voice": ["clinical", "empathetic", "premium", "casual", "bold", "..."],
"consistency_check": "visuals support/undermine claims because ...",
"voc_alignment": ["aligns with ", "mismatch: "],
"citations": ["url1", "url2", "..."],
"screenshots": ["path_or_url_if_Browserbase", "..."]
}
```

## 3) Pricing & Offer Mechanics (Brand or Competitor)

**When:** Prompt 2, Step 5–7

**Inputs:** {{brand_or_competitor}}, URLs

**Query**

Extract offer mechanics: price points, bundles, subscriptions, trials, guarantees, financing, shipping thresholds, returns policy. Capture exact phrasing used near CTAs.

**Output Schema**

```json
{
"entity": "{{brand_or_competitor}}",
"offers": [
{"sku":"...", "price":"$...", "bundle":"...", "sub":".../mo", "trial":"...", "guarantee":"..."}
],
"cta_copy": ["", ""],
"policy_highlights": ["shipping", "returns", "warranty"],
"citations": ["url1", "url2", "..."]
}
```

## 4) VoC Mining — Reviews (CSV / Marketplace / Web)

**When:** Prompt 1 (Step 4B), Prompt 3 (objections), Prompt 4 (angles)

**Inputs:** {{BRAND_NAME}}, {{category}}, product names, marketplace pages

**Query**

Gather verbatim review snippets (positive/negative/neutral). Extract recurring phrases and score frequency × emotional intensity. Tag pre-purchase vs post-purchase themes. Flag metaphors, identity conflicts, shame/guilt/fear/relief language.

**Output Schema**

```json
{
"samples": [
{"quote":"", "sentiment":"pos/neg/neu", "source":"[CSV]/[Apify]/[External]", "url":"...", "pre_post":"pre/post"}
],
"recurring_phrases_ranked": [
{"phrase":"...", "frequency":1, "intensity":1, "examples":[0,1]}
],
"themes": {
"fear":["...", "..."],
"hope":["...", "..."],
"guilt":["...", "..."],
"pride":["...", "..."]
},
"metaphors": ["...", "..."],
"identity_conflicts": ["I want X but Y", "..."]
}
```

## 5) VoC Mining — Reddit (UGC)

**When:** Prompt 1 (Step 4B), Prompt 3

**Inputs:** subreddits, {{brand}}, {{category}}, {{product}}

**Query**

Search Reddit for {{brand}}, {{category}}, {{product}}. Pull at least 6 high-signal quotes that show doubts, desires, regret, delight, social signaling, or practical hurdles. Prefer parent comments with context.

**Output Schema**

```json
{
"reddit_quotes": [
{"quote":"", "thread":"url", "subreddit":"...", "topic":"fear/hope/guilt/pride", "notes":"identity cue, metaphor, trigger"}
]
}
```

## 6) VoC Mining — YouTube Transcripts

**When:** Prompt 1 (Step 4B), Prompt 4 (proof/story angles)

**Inputs:** query terms, channel URLs

**Query**

Fetch transcripts for top review/tutorial/comparison videos around {{brand}} or {{category}}. Extract 2+ crisp proof lines + before/after moments.

**Output Schema**

```json
{
"yt_snippets": [
{"quote":"", "video":"url", "channel":"...", "moment":"proof/before-after/how-to"}
]
}
```

## 7) Awareness Triggers & Moment-of-Need Language

**When:** Prompt 1 (ICPs), Prompt 3 (Motivation Map)

**Inputs:** {{category}}, life events, seasonality

**Query**

Mine language that signals problem crystallization (e.g., "we ran out of space," "kids bored indoors," "too many tiny pieces," "cleanup takes forever"). Capture situational/seasonal triggers and the exact phrases used.

**Output Schema**

```json
{
"triggers": [
{"situation":"...", "season":"...", "phrase":"", "source":"...", "url":"..."}
]
}
```

## 8) Objection Discovery & Rebuttal Levers

**When:** Prompt 3, Step 2

**Inputs:** VoC from Prompt 1, competitor claims from Prompt 2

**Query**

Identify 5–10 dominant objections (cost, quality, trust, complexity, longevity, space, returns). For each: emotional root, logical surface reason, and potential copy/proof/offer response. Use customer language.

**Output Schema**

```json
{
"objections": [
{"objection":"", "emotional_root":"shame/fear/overwhelm", "logical_reason":"...", "response":"headline + proof element", "citations":["..."]}
]
}
```

## 9) Differentiation & White Space

**When:** Prompt 2, Step 8; Prompt 4 (pillars)

**Inputs:** competitor matrices + VoC

**Query**

From the comparison + VoC gaps, list 3–5 differentiation opportunities (emotional + functional). For each, explain why it matters (VoC link) and how to activate (pillar angle, proof, channel).

**Output Schema**

```json
{
"opportunities_ranked": [
{"opportunity":"...", "why":"...", "activation":"pillar/story/proof/channel", "evidence":["..."]}
]
}
```

## 10) SEO & SERP Context (optional)

**When:** Prompt 2; only if SEO is in scope

**Inputs:** {{brand}}, {{category}}

**Query**

Retrieve SERP competitors, top queries, and CPC/intent for category head terms. Map which competitors dominate search vs socials vs marketplaces.

**Output Schema**

```json
{
"serp": {
"top_terms":[{"term":"...", "volume":1, "cpc":"$...", "intent":"informational/commercial"}],
"serp_competitors":["...", "..."],
"notes":"..."
}
}
```

## 11) Browserbase Capture (escalation)

**When:** Any step where pages are JS-rendered/blocked

**Inputs:** target URL(s)

**Query**

Render the page, wait for key selectors (hero, PDP bullets, reviews), extract visible text, and take a first-screen screenshot. Save both and return paths.

**Output Schema**

```json
{
"browserbase_capture": {
"url":"...",
"rendered_text_path":"...",
"screenshot_path":"...",
"selectors_hit":["...", "..."],
"timestamp":"ISO8601"
}
}
```

## 12) Copywriter Synthesis (Narrative Pass)

**When:** End of Prompts 1, 3, 4

**Inputs:** VoC Enrichment, objections, pillars

**Query**

Write a one-page narrative in customer language using verbatim quotes. Provide 3 hook headlines per ICP, 5 objection-handling lines (headline + 1-sentence proof), and a Do/Don't tone guide (5 each).

**Output Schema**

```json
{
"copy_brief": {
"narrative":"...",
"hooks_per_icp": {"Strangers":["...", "..."], "Audience":["..."], "Customers":["..."]},
"objection_lines":[{"headline":"...", "proof":"..."}],
"tone_do":["...", "..."],
"tone_dont":["...", "..."]
}
}
```

## 13) Targeted Follow-Up Queries (for Evidence Quotas)

### Pricing & Value Anxiety
- "is {{brand}} worth it reddit"
- "{{product}} price vs competitors"
- "{{category}} best value 2025 forum"

### Durability & Regret
- "{{product}} durability problems reddit"
- "{{brand}} returns policy experience"
- "{{category}} broke after a week review"

### Identity & Social Proof
- "why parents choose {{brand}} reddit"
- "alternatives to {{brand}}"
- "instagram tiktok {{brand}} review transcript"

### Offer Mechanics & Trust
- "{{brand}} discount code policy"
- "{{brand}} warranty complaints"
- "{{brand}} shipping delay reddit"

---

## Notes

When using these templates, persist raw captures to `/outputs/{{RUN_DATE}}_{{BRAND_NAME}}/raw/`.

If a field is unknown, fill with "Gap" and add the URL or next query to run.