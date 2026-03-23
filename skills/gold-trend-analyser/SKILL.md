---
name: gold-trend-analyser
description: >
  Performs deep technical and fundamental analysis of gold price trends and generates a
  polished, self-contained HTML report with buy/sell/hold recommendations plus short,
  medium, and long-term forecasts. Use this skill whenever a user asks about gold price
  analysis, gold investment recommendations, XAU/USD trends, gold market outlook, gold
  trading signals, precious metals analysis, or any request to analyse or forecast gold
  prices. Trigger even for casual phrasings like "should I buy gold?", "how's gold doing?",
  "is gold a good investment now?", or "gold price prediction". Always produce an HTML report.
---

# Gold Price Trend Analyser Skill

## Purpose
Fetch live gold price data, run multi-timeframe technical + fundamental analysis, and
render a comprehensive self-contained HTML report with:
- Current price snapshot & daily change
- Technical indicators (RSI, MACD, Bollinger Bands, Moving Averages, ATR, Stochastic)
- Support & resistance levels
- Trend strength (ADX)
- Fundamental drivers (USD strength, real yields, geopolitics, inflation)
- Buy / Sell / Hold recommendation with confidence score
- Short-term (1–4 weeks), medium-term (1–6 months), and long-term (6–24 months) forecasts
- Interactive price chart (Chart.js)
- Risk assessment table

---

## Workflow

### Step 1 — Fetch Gold Price Data
Use **web_search** to collect current gold price data. Run these searches in parallel:

```
web_search("XAU/USD gold price today live")
web_search("gold price technical analysis RSI MACD 2026")
web_search("gold price forecast short term 2026")
web_search("gold price forecast long term 2026")
web_search("gold fundamental drivers USD inflation real yields 2026")
web_search("gold support resistance levels today")
```

Collect at minimum:
- Current spot price (USD/oz)
- 24h change ($ and %)
- Recent price range (1-week, 1-month, 3-month highs/lows)
- Any RSI, MACD, or MA values cited in sources
- Analyst price targets
- Key macro drivers mentioned

### Step 2 — Run Analysis

Using collected data, compute or derive the following. Where exact values aren't available
from search, use reasonable estimates based on context and clearly mark them as "estimated".

#### Technical Analysis Checklist
- [ ] Trend direction (bullish/bearish/neutral) across 3 timeframes
- [ ] RSI(14): overbought >70, oversold <30
- [ ] MACD: signal line crossover status
- [ ] 50-day & 200-day MA: price position relative to each; golden/death cross?
- [ ] Bollinger Bands: is price near upper/lower band?
- [ ] Key support levels (2–3 levels)
- [ ] Key resistance levels (2–3 levels)
- [ ] Volume trend (if available)
- [ ] ATR (volatility measure)

#### Fundamental Analysis Checklist
- [ ] USD Index (DXY) trend — inverse correlation with gold
- [ ] US 10-year real yield trend — inverse correlation with gold
- [ ] Inflation expectations (CPI, PCE)
- [ ] Central bank buying/selling activity
- [ ] Geopolitical risk premium
- [ ] ETF flow trend (GLD, IAU holdings)
- [ ] Seasonal patterns (gold typically strong Q4, Q1)

#### Scoring the Recommendation
Weight technicals 50%, fundamentals 50%.

| Signal | Bullish (+1) | Neutral (0) | Bearish (-1) |
|--------|-------------|-------------|--------------|
| RSI | <40 | 40–60 | >70 |
| Price vs 200MA | Above | At | Below |
| MACD | Bullish cross | Neutral | Bearish cross |
| DXY | Falling | Flat | Rising |
| Real Yields | Falling | Flat | Rising |
| Inflation | Rising | Stable | Falling |
| Geopolitics | High risk | Moderate | Low risk |
| CB Buying | Accelerating | Steady | Slowing |

Sum scores → divide by 8 → scale -100 to +100:
- +40 to +100: **BUY** 🟢
- -39 to +39: **HOLD** 🟡  
- -40 to -100: **SELL** 🔴

Confidence = `abs(score) * 1.25` capped at 95%

### Step 3 — Generate Forecasts

Structure forecasts as price ranges with a base case and bull/bear scenarios:

**Short-term (1–4 weeks)**
- Based on: technical momentum, upcoming economic events, short-term positioning
- Format: Low / Base / High price target

**Medium-term (1–6 months)**
- Based on: macro trends, Fed policy direction, seasonal patterns, ETF flows
- Format: Low / Base / High price target

**Long-term (6–24 months)**
- Based on: structural drivers (de-dollarisation, CB reserves, real yield outlook)
- Format: Low / Base / High price target

### Step 4 — Build the HTML Report

Generate a single self-contained HTML file. See the HTML template spec in
`references/html-template-spec.md` for the exact structure.

Save the report to `/mnt/user-data/outputs/gold-analysis-report.html`

Then call `present_files` with the output path.

---

## Report Requirements

The HTML report MUST include:

1. **Header bar** — Gold logo icon, title, timestamp, current price + change badge
2. **Executive Summary card** — Recommendation (BUY/SELL/HOLD), confidence %, one-paragraph rationale
3. **Price Chart** — Interactive line chart using Chart.js showing simulated recent price action
   with support/resistance horizontal lines
4. **Technical Indicators panel** — Gauge/badge for each indicator with value + signal
5. **Fundamental Drivers panel** — Table of macro factors with impact direction and commentary
6. **Support & Resistance table** — Clearly marked levels with strength ratings
7. **Forecast section** — Three cards (short/medium/long) each with bear/base/bull scenarios,
   price range bar, and key assumptions
8. **Risk Assessment table** — Key risks with probability (Low/Med/High) and potential impact
9. **Disclaimer footer** — "For informational purposes only. Not financial advice."

### Visual Design Standards
- Dark theme preferred (`#0a0a0f` background, gold accents `#FFD700` / `#FFA500`)
- Use CSS Grid and Flexbox for layout — fully responsive
- Colour-code: green (#22c55e) = bullish, red (#ef4444) = bearish, yellow (#eab308) = neutral
- Animate metric cards on load (CSS keyframe fade-in)
- No external dependencies except Chart.js from CDN

---

## Quality Gates

Before saving the file, verify:
- [ ] All price figures are from searches (or clearly marked estimated)
- [ ] Recommendation is explicitly justified by the scoring table
- [ ] All three forecast timeframes have bear/base/bull scenarios
- [ ] HTML is valid and self-contained (no broken external links except Chart.js CDN)
- [ ] Disclaimer is present
- [ ] File size < 500KB

---

## Error Handling

If web search returns no price data:
- Use the most recent price from your training knowledge
- Mark prominently in report: "⚠️ Live data unavailable — using estimated values"
- Still generate the full report

If Chart.js CDN fails to load:
- The chart container should show a graceful fallback message
- All other panels should still render correctly

---

## Example Invocations

User says → Skill should trigger:
- "Analyse gold price and tell me if I should buy" → full report
- "Gold trend analysis" → full report
- "Is gold bullish or bearish right now?" → full report
- "Give me a gold price forecast for the next 6 months" → full report
- "XAU/USD technical analysis" → full report
- "Should I invest in gold?" → full report

---

## See Also

- `references/html-template-spec.md` — Detailed HTML structure and CSS template
- `references/indicator-formulas.md` — Technical indicator calculation reference
