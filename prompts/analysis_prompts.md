# Market Analysis LLM Prompts

This file contains the prompt templates used by the n8n workflow for market analysis.

## 1. News Analysis & Urgency Scoring

```
You are an expert financial analyst and market researcher. Analyze the following news items and provide:

1. **URGENCY SCORE** (1-10): Rate the overall market importance. 8+ means immediate alert needed.
   - 10: Black swan event (war outbreak, major market crash, pandemic)
   - 8-9: Significant market-moving event (major central bank surprise, geopolitical escalation)
   - 6-7: Notable news worth monitoring
   - 1-5: Routine market news

2. **KEY THEMES**: Identify 3-5 dominant themes across the news

3. **MARKET IMPACT SUMMARY**: Brief analysis of potential market implications

4. **SECTOR ALERTS**: Which sectors are most affected (positive/negative)

5. **COMMODITIES OUTLOOK**: Impact on gold, oil, and other key commodities

6. **RISK ASSESSMENT**: Current risk-on or risk-off environment

News Items:
[NEWS_ITEMS_HERE]

Provide your analysis in a structured JSON format with these exact keys: urgencyScore, keyThemes, marketImpact, sectorAlerts, commoditiesOutlook, riskAssessment
```

## 2. Urgent Alert Generation

```
URGENT MARKET ALERT - Generate an immediate action briefing.

Urgency Score: [SCORE]/10

Key Themes: [THEMES]

Market Impact: [IMPACT]

Sector Alerts: [SECTORS]

Write a concise but comprehensive URGENT ALERT email for an investor with an 80/20 aggressive portfolio (equities + commodities, global macro, diversified sectors). Include:

1. **ALERT HEADLINE** (attention-grabbing, factual)
2. **SITUATION SUMMARY** (2-3 sentences on what happened)
3. **IMMEDIATE IMPLICATIONS** (what this means for markets)
4. **RECOMMENDED ACTIONS** (specific, actionable steps - buy/sell/hold/hedge recommendations)
5. **RISK LEVEL** (current portfolio risk assessment)
6. **MONITORING POINTS** (what to watch in the next 24-48 hours)

Format as HTML email with proper styling. Be direct and actionable.
```

## 3. Weekly Report Generation

```
You are a senior investment analyst preparing a comprehensive WEEKLY MARKET REPORT for a client with the following profile:

**INVESTOR PROFILE:**
- Risk Tolerance: 80/20 Aggressive (80% equities, 20% commodities/alternatives)
- Geographic Focus: Global Macro (US, EU, Asia, Emerging Markets)
- Asset Classes: Equities + Commodities
- Sectors: Diversified
- Trading Platforms: Trading Republic, Interactive Brokers

**THIS WEEK'S DATA:**
[WEEKLY_DATA_JSON]

Generate a comprehensive weekly report with the following sections:

## 1. EXECUTIVE DASHBOARD
- Overall Market Sentiment: [Bullish/Neutral/Bearish]
- Risk Environment: [Risk-On/Risk-Off/Mixed]
- Recommended Portfolio Action: [Accumulate/Hold/Reduce/Defensive]
- Key Number of the Week: [Most important statistic]

## 2. GLOBAL MACRO OVERVIEW
- US Markets Analysis
- European Markets Analysis
- Asian Markets Analysis
- Emerging Markets Spotlight

## 3. SECTOR ANALYSIS
- Winners of the Week (with rationale)
- Losers of the Week (with rationale)
- Sectors to Watch

## 4. COMMODITIES REPORT
- Gold & Precious Metals
- Energy (Oil, Natural Gas)
- Industrial Metals
- Agricultural (if relevant)

## 5. INVESTMENT RECOMMENDATIONS
### BUY Recommendations (3-5 specific tickers)
For each: Ticker, Current Context, Entry Zone, Risk Level

### HOLD/MONITOR List
Positions to maintain or watch

### SELL/AVOID Recommendations
What to reduce exposure to

## 6. RISK FACTORS & WATCHLIST
- Key risks for the coming week
- Important dates (earnings, economic data, events)
- Scenarios to monitor

## 7. PORTFOLIO ALLOCATION SUGGESTION
Suggested allocation breakdown for an 80/20 portfolio this week

Format as a professional HTML email with clean styling, tables where appropriate, and clear visual hierarchy.
```

## 4. Knowledge Base Summary (for GitHub storage)

```
Summarize the following market analysis for long-term knowledge storage. Extract:

1. Key market events and their outcomes
2. Successful and unsuccessful predictions
3. Notable correlations observed
4. Lessons learned
5. Updated market regime assessment

Keep the summary concise (under 500 words) but information-dense. This will be used to inform future analyses.

[ANALYSIS_DATA]
```

---

## Customization Notes

- Adjust urgency thresholds based on your personal risk tolerance
- Add specific tickers to monitor in the prompts if you build a portfolio
- Modify sector focus by editing the "diversified" parameter
- Geographic focus can be narrowed by specifying regions in the prompts
