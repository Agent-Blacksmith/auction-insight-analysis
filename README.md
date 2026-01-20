# Unlocking Google Ads Competitive Analysis with AI Agents

**Competitive Intelligence Engine for Google Ads using n8n + Apify + AI**

![alt text](https://agentblacksmith.com/wp-content/uploads/2026/01/agent-builder-vishal-landscape-scaled-e1768846301365.png)

This repository contains an end-to-end **competitive intelligence workflow** built in **n8n**.
It combines **Google Ads Auction Insights**, **keyword performance**, **live SERP scraping**, and **AI-driven analysis** to identify **who your real competitors are**, **where they show up**, and **how they win**.

This is not a dashboard.
It is a **decision system**.

I figured it would be a fun weekend project. Part of my AI learning journey and maybe 10 hours max, grab a coffee, build an agent, done!

**Narrator voice: It took 50 hours.**

I have attached the n8n json for your reference in this git. More info on my journey read [auction insights ai agent](https://agentblacksmith.com/google-ads-auction-analysis-ai-agent/).

---
# Quick Start

1. Sign up to n8n, apify free plan and openrouter free account
2. In n8n, import the json file from above, or copy paste it in the workflow
3. For apify nodes, setup the credentials
4. For ai model nodes, setup openrouter and feel free to use a free ai model or add credits for something more robust
5. Run the workflow and slay your competitors!

---
## What this workflow does

At a high level, the workflow:

1. Ingests Google Ads exports
2. Identifies **high-impact keywords**
3. Filters **real competitors** using Auction Insights metrics
4. Scrapes **live paid SERPs** multiple times
5. Extracts **ad copy and landing pages**
6. Scores competitors based on **threat and consistency**
7. Uses AI to generate **actionable competitive insights**
8. Sends a **plain-text intelligence report by email**

---

## Inputs Required

The workflow starts with a **Form Trigger** and requires the following inputs.

### Mandatory

* **Email**
  Used to send the final intelligence report

* **Auction Insights report**
  Google Ads export
  Must be keyword-segmented

* **Keyword Performance report**
  Google Ads export
  Used to score importance

* **Ad Report**
  Google Ads export
  Used to enrich RSA copy and final URLs

### Optional Controls

* Importance metric
  impressions
  clicks
  conversions
  weighted

* Competitor filter metric
  search impression share
  overlap rate
  position above rate
  outranking share
  top of page rate
  absolute top of page rate

* Thresholds
  minimum impressions
  minimum cost
  competitor metric cutoff

---

## Core Logic Overview

### 1. Normalize and merge Google Ads data

* Auction Insights
* Keyword performance
* Ad level assets

All rows are normalized into a **keyword-centric structure**.

---

### 2. Identify meaningful competitors

Competitors are filtered using:

* Auction Insights metrics
* Configurable thresholds
* Keyword importance weighting

Keywords with no meaningful competition are discarded early.

---

### 3. Rank keywords by strategic importance

Keywords are scored using:

* Raw volume or conversions
* Weighted importance
* Competitive breadth

Only the **top keywords** move forward.

---

### 4. Multi-pass live SERP scraping

For each selected keyword:

* Pass 1: generic query
* Pass 2–3: brand-modified queries

This avoids false negatives caused by:

* Auction rotation
* Budget pacing
* Geo variance

---

### 5. Paid ad extraction and validation

From live SERPs:

* Paid ads only
* Root domain normalization
* Best ad per competitor
* Appearance consistency across passes

This answers:

> Are they actually advertising, or just appearing once?

---

### 6. Threat rescoring

Competitors are rescored using:

* Auction Insights threat score
* Live SERP presence
* Cross-run consistency

Result:
A **prioritized competitor list** per keyword.

---

### 7. Landing page scraping

* Competitor landing pages
* Your landing page
* Text-only extraction
* Scripts, images, and noise removed

This keeps prompts token-efficient and analysis focused.

---

### 8. AI competitive analysis

For each keyword:

* Competitor ad tactics
* Landing page tactics
* Positioning patterns
* Gaps vs your offering
* Actionable recommendations

The AI is instructed to:

* Compare strategies
* Avoid fluff
* Produce operational insights

---

### 9. Report aggregation and delivery

All outputs are consolidated into a **single plain-text report** and emailed to the user.

No dashboards.
No PDFs.
Readable in any inbox.

---

## Caching Strategy

To reduce cost and noise:

* Paid SERP results are cached using **n8n Data Tables**
* Cache key includes:

  * keyword
  * country
  * device
  * scrape pass
* Cache TTL is configurable
* Stale entries are automatically refreshed

---

## Required Credentials

You must configure the following in n8n:

* **Apify API**
* **Brevo SendInBlue API**
* **LLM provider**
  via OpenRouter or equivalent

All credential IDs in the workflow are placeholders.

---

## Setup Instructions

1. Import the workflow JSON into n8n
2. Replace placeholder IDs:

   * `YOUR_WEBHOOK_ID`
   * `YOUR_APIFY_CREDENTIAL_ID`
   * `YOUR_DATA_TABLE_ID`
   * `YOUR_BREVO_CREDENTIAL_ID`
3. Create a Data Table named `paid_ads_cache`
4. Ensure Google Ads exports use:

   * UTF-16
   * Tab-delimited
   * Header row starting on line 3
5. Run once manually before sharing publicly

---

## What this is **not**

* Not a replacement for Auction Insights UI
* Not a keyword planner
* Not a competitor list scraper
* Not a vanity dashboard

This system answers:

> Which competitors actually matter, where, and why?

---

## Who this is for

* Performance marketers
* Growth teams
* Paid search specialists
* Competitive intelligence builders
* AI-first marketing operators

If you manage large Google Ads accounts, this saves hours of manual work per analysis.

---

## Status

Actively evolving
Designed to be forked, modified, and extended

## Why I'm Sharing This (AgentBlacksmith)
My goal this year is to **Build, Execute, and Share**.

I’m starting **AgentBlacksmith.com** to document this journey of building real, useful AI agents. No fluff, just building.
