# MarketAnalyst

Automated market research and investment intelligence system powered by n8n and Google Gemini.

## Overview

MarketAnalyst is an automated workflow that:
- Scrapes global financial news from free sources (Google News, Yahoo Finance, Reddit)
- Analyzes market conditions using Google Gemini AI
- Sends urgent alerts when significant events occur (urgency score 8+/10)
- Delivers comprehensive weekly investment reports
- Stores all analysis in GitHub as a persistent knowledge base

## Investor Profile

| Parameter | Setting |
|-----------|---------|
| Risk Tolerance | 80/20 Aggressive |
| Geographic Focus | Global Macro |
| Asset Classes | Equities + Commodities |
| Sectors | Diversified |
| Platforms | Trading Republic, Interactive Brokers |

## Workflow Components

### 1. News Aggregation (Every 6 hours)
- Google News (Markets, Geopolitics, Commodities)
- Yahoo Finance RSS
- Reddit sentiment (r/wallstreetbets, r/investing)
- VIX volatility monitoring

### 2. Alert System
- Urgency scoring (1-10 scale)
- Immediate email for score 8+ events
- Black swan detection (war, crashes, pandemics)

### 3. Weekly Report (Sundays 8AM)
- Executive dashboard
- Global macro overview
- Sector analysis
- Commodities report
- Buy/Sell/Hold recommendations
- Portfolio allocation suggestions

### 4. Knowledge Base
- Reports stored in `reports/YYYY/week_XX.md`
- Alerts stored in `alerts/YYYY-MM-DD_alert.json`

## Quick Start

1. Import `workflows/market_research_workflow.json` into n8n
2. Configure credentials (see `docs/SETUP_GUIDE.md`)
3. Set environment variables
4. Activate the workflow

## Repository Structure

```
MarketAnalyst/
├── workflows/           # n8n workflow JSON files
├── prompts/            # LLM prompt templates
├── docs/               # Setup documentation
├── reports/            # Weekly analysis reports (auto-generated)
├── alerts/             # Urgent alert archives (auto-generated)
└── memory              # Knowledge base for AI context
```

## Requirements

- n8n (self-hosted or cloud)
- Google Gemini Pro subscription (API access)
- GitHub account
- SMTP email access

## Cost

$0/month with existing Gemini Pro subscription and self-hosted n8n.

## Documentation

- [Setup Guide](docs/SETUP_GUIDE.md) - Complete installation instructions
- [Prompt Templates](prompts/analysis_prompts.md) - Customizable LLM prompts
