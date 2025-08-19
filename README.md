# Brand Brief Generator

**Automated brand research and messaging framework generation using AI-powered web crawling and analysis.**

Transform any brand into comprehensive marketing briefs with deep customer insights, competitive analysis, and strategic messaging frameworks - all generated automatically from web sources and customer reviews.

## What It Does

This tool automates the entire brand brief creation process, generating:

- **Deep Customer Voice Research** - Customer pain points, motivations, and language patterns
- **Competitive Landscape Analysis** - Market positioning, differentiation opportunities, and competitor messaging
- **Purchase Motivation Framework** - Emotional drivers, decision factors, and brand perception mapping
- **Strategic Messaging Pillars** - Core value propositions, content themes, and campaign messaging

## Perfect For

- **Marketing Teams** - Generate campaign-ready brand briefs in hours, not weeks
- **Agencies** - Scale brand research across multiple clients efficiently
- **Startups** - Understand your market position and customer voice quickly
- **Product Teams** - Align messaging with customer needs and competitive landscape

## How It Works

1. **Configure Sources** - Add brand website, social media, and competitor URLs
2. **Add Customer Reviews** (Optional) - Upload CSV with customer feedback for deeper insights
3. **Run Workflow** - Execute 4-step AI analysis pipeline
4. **Get Results** - Receive comprehensive brand brief with actionable insights

## Quick Start

1. **Install Cursor Desktop** and configure MCP servers
2. **Fill brand sources** in `/docs/brand_sources.md`
3. **Run workflow**: `/run 00_master_workflow.md`
4. **Review outputs** in the generated folders

## Requirements

- **Cursor Desktop** with MCP servers:
  - `firecrawl-mcp` (web scraping)
  - `perplexity-mcp` (insight synthesis)
  - `tavily-remote-mcp` (targeted research)
  - `apify` (optional, for social/review scraping)

## Features

- **AI-Powered Analysis** - Uses multiple AI models for comprehensive research
- **Web Crawling** - Automatically scrapes brand websites, social media, and competitor content
- **Customer Voice Integration** - Incorporates real customer reviews when available
- **Structured Outputs** - Clean, markdown-formatted reports ready for marketing teams
- **Iterative Refinement** - Self-expanding analysis until comprehensive insights are generated
- **Multi-Brand Support** - Run for different brands with automatic folder organization

## Workflow

The system executes a 4-step pipeline:

1. **Customer Voice Research** → Deep analysis of customer needs and language
2. **Competitive Landscape** → Market positioning and differentiation analysis  
3. **Purchase Motivations** → Emotional drivers and decision framework
4. **Messaging Strategy** → Core messaging pillars and content themes

Each step builds on previous outputs, ensuring comprehensive and coherent results.

## Use Cases

- **Brand Positioning** - Understand your market position and differentiation opportunities
- **Campaign Development** - Generate messaging frameworks for marketing campaigns
- **Customer Research** - Deep dive into customer pain points and motivations
- **Competitive Analysis** - Monitor competitor messaging and market trends
- **Content Strategy** - Develop content themes aligned with customer needs

---

**Ready to generate your first brand brief?**Download the brand brief generator repo today!

---

*Built with ❤️ for marketing teams who want to move faster and smarter.*
