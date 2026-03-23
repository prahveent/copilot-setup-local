# HTML Report Template Specification

## File Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gold Price Analysis Report — [DATE]</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
  <style>/* ALL CSS inline here */</style>
</head>
<body>
  <!-- 1. Header -->
  <!-- 2. Executive Summary -->
  <!-- 3. Price Chart -->
  <!-- 4. Technical Indicators -->
  <!-- 5. Fundamental Drivers -->
  <!-- 6. Support & Resistance -->
  <!-- 7. Forecasts -->
  <!-- 8. Risk Assessment -->
  <!-- 9. Footer / Disclaimer -->
  <script>/* ALL JS inline here — Chart.js setup + animations */</script>
</body>
</html>
```

---

## Section 1: Header Bar

```html
<header class="header">
  <div class="header-left">
    <span class="gold-icon">◈</span>
    <div>
      <h1>Gold Price Analysis</h1>
      <span class="timestamp">Generated: [DATETIME] UTC</span>
    </div>
  </div>
  <div class="header-right">
    <div class="price-badge">
      <span class="price">$[PRICE]</span>
      <span class="change [up|down]">[+/-][CHANGE] ([PCT]%)</span>
    </div>
    <span class="pair-label">XAU/USD · Troy Oz</span>
  </div>
</header>
```

---

## Section 2: Executive Summary Card

```html
<section class="exec-summary">
  <div class="recommendation-badge [buy|sell|hold]">
    <span class="rec-icon">[🟢|🔴|🟡]</span>
    <span class="rec-label">[BUY|SELL|HOLD]</span>
    <span class="rec-conf">[CONFIDENCE]% Confidence</span>
  </div>
  <div class="summary-text">
    <h2>Executive Summary</h2>
    <p>[2–3 sentence rationale covering technicals + fundamentals + key risk]</p>
  </div>
  <div class="score-bar">
    <div class="score-fill" style="width:[ABS_SCORE]%; background:[COLOR]"></div>
    <span class="score-label">Signal Strength: [SCORE]/100</span>
  </div>
</section>
```

---

## Section 3: Price Chart

```html
<section class="chart-section">
  <h2>Price Action (90-Day Simulated)</h2>
  <div class="chart-wrapper">
    <canvas id="priceChart"></canvas>
  </div>
</section>
```

**Chart.js Config:**
- Type: `line`
- Dataset: ~90 price points (generate realistic simulated OHLC from current price + known range)
- Show two horizontal lines for nearest support + nearest resistance using annotation plugin
  or drawn via `afterDraw` plugin hook
- Colour: gold line (`#FFD700`), filled gradient to transparent
- Grid: dark (`rgba(255,255,255,0.05)`)
- Tooltip: show price, date

Generate ~90 data points by:
1. Take current price as endpoint
2. Walk backwards using known 1-month and 3-month high/low as anchors
3. Add mild noise: `price += (Math.random() - 0.48) * dailyVolatility`
4. Where `dailyVolatility ≈ ATR` or roughly `currentPrice * 0.007`

---

## Section 4: Technical Indicators Panel

```html
<section class="indicators-grid">
  <h2>Technical Indicators</h2>
  <div class="grid-4">
    <!-- Repeat for each indicator -->
    <div class="indicator-card [bullish|bearish|neutral]">
      <div class="ind-name">RSI (14)</div>
      <div class="ind-value">[VALUE]</div>
      <div class="ind-signal">[SIGNAL TEXT]</div>
      <div class="ind-bar"><div class="ind-fill" style="width:[PCT]%"></div></div>
    </div>
  </div>
</section>
```

**Indicators to include (8 cards):**

| Card | Name | Value Format | Signal Logic |
|------|------|-------------|--------------|
| 1 | RSI (14) | 0–100 | <30 Oversold 🟢, 30–50 Mildly Bearish, 50–70 Mildly Bullish, >70 Overbought 🔴 |
| 2 | MACD | +/- value | Above signal = Bullish 🟢, Below = Bearish 🔴 |
| 3 | 50-Day MA | $price | Price above = Bullish, below = Bearish |
| 4 | 200-Day MA | $price | Price above = Bullish (golden cross?), below = Bearish |
| 5 | Bollinger Bands | Upper/Lower | Near upper = overbought, lower = oversold |
| 6 | Stochastic %K | 0–100 | <20 oversold, >80 overbought |
| 7 | ATR (14) | $value | Volatility gauge: Low/Medium/High |
| 8 | ADX | 0–100 | <25 weak trend, 25–50 moderate, >50 strong |

---

## Section 5: Fundamental Drivers

```html
<section class="fundamentals">
  <h2>Fundamental Drivers</h2>
  <table class="fund-table">
    <thead>
      <tr><th>Driver</th><th>Current Status</th><th>Impact on Gold</th><th>Commentary</th></tr>
    </thead>
    <tbody>
      <!-- One row per driver -->
      <tr class="[bull|bear|neutral]-row">
        <td>[DRIVER NAME]</td>
        <td>[VALUE/STATUS]</td>
        <td><span class="impact-badge [bull|bear|neutral]">[↑ Bullish|↓ Bearish|→ Neutral]</span></td>
        <td>[1 sentence commentary]</td>
      </tr>
    </tbody>
  </table>
</section>
```

**Drivers to include (6–8 rows):**
1. US Dollar Index (DXY)
2. US 10Y Real Yield
3. CPI / Inflation Expectations
4. Central Bank Net Buying
5. Geopolitical Risk Index
6. Gold ETF Flows (GLD/IAU)
7. Fed Policy Outlook
8. Seasonal Pattern

---

## Section 6: Support & Resistance

```html
<section class="sr-section">
  <h2>Support & Resistance Levels</h2>
  <div class="sr-grid">
    <div class="resistance-col">
      <h3>🔴 Resistance</h3>
      <!-- 3 levels -->
      <div class="sr-level strong">
        <span class="sr-price">$[PRICE]</span>
        <span class="sr-label">R3 — [Description]</span>
        <div class="sr-strength-bar" style="width:90%"></div>
      </div>
    </div>
    <div class="current-price-marker">Current: $[PRICE]</div>
    <div class="support-col">
      <h3>🟢 Support</h3>
      <!-- 3 levels -->
    </div>
  </div>
</section>
```

---

## Section 7: Forecasts

```html
<section class="forecast-section">
  <h2>Price Forecasts</h2>
  <div class="forecast-grid">

    <div class="forecast-card short-term">
      <div class="fc-header">
        <span class="fc-icon">⚡</span>
        <h3>Short-Term</h3>
        <span class="fc-period">1–4 Weeks</span>
      </div>
      <div class="scenario-bars">
        <div class="scenario bear">
          <span class="sc-label">Bear</span>
          <span class="sc-price">$[LOW]</span>
          <div class="sc-bar" style="width:30%"></div>
        </div>
        <div class="scenario base highlighted">
          <span class="sc-label">Base</span>
          <span class="sc-price">$[BASE]</span>
          <div class="sc-bar" style="width:65%"></div>
        </div>
        <div class="scenario bull">
          <span class="sc-label">Bull</span>
          <span class="sc-price">$[HIGH]</span>
          <div class="sc-bar" style="width:90%"></div>
        </div>
      </div>
      <div class="fc-assumptions">
        <strong>Key Assumptions:</strong>
        <ul>
          <li>[Assumption 1]</li>
          <li>[Assumption 2]</li>
        </ul>
      </div>
      <div class="fc-catalyst">🎯 Key Catalyst: [EVENT]</div>
    </div>

    <!-- Repeat for Medium-Term (1–6 Months) and Long-Term (6–24 Months) -->

  </div>
</section>
```

---

## Section 8: Risk Assessment

```html
<section class="risk-section">
  <h2>Risk Assessment</h2>
  <table class="risk-table">
    <thead>
      <tr><th>Risk Factor</th><th>Direction</th><th>Probability</th><th>Impact</th><th>Commentary</th></tr>
    </thead>
    <tbody>
      <tr>
        <td>[RISK NAME]</td>
        <td><span class="dir-badge [up|down]">[Upside|Downside]</span></td>
        <td><span class="prob-badge [low|med|high]">[Low|Medium|High]</span></td>
        <td><span class="impact-badge [low|med|high]">[Low|Medium|High]</span></td>
        <td>[Commentary]</td>
      </tr>
    </tbody>
  </table>
</section>
```

**Risks to include (6 rows):**
1. USD Strengthening Surprise (Downside)
2. Fed Rate Hike Surprise (Downside)
3. Escalating Geopolitical Crisis (Upside)
4. Inflation Re-acceleration (Upside)
5. Central Bank Selling (Downside)
6. Risk-Off Flight to Safety (Upside)

---

## Section 9: Footer

```html
<footer class="report-footer">
  <div class="data-sources">
    <strong>Data Sources:</strong> [LIST SOURCES USED]
  </div>
  <div class="disclaimer">
    ⚠️ <strong>Disclaimer:</strong> This report is generated for informational and educational 
    purposes only. It does not constitute financial advice, investment recommendations, or an 
    offer to buy or sell any securities or commodities. Gold trading involves substantial risk 
    of loss. Past price patterns do not guarantee future results. Always consult a qualified 
    financial advisor before making investment decisions.
  </div>
  <div class="generated-by">
    Generated by Gold Trend Analyser Skill · Powered by Claude AI
  </div>
</footer>
```

---

## CSS Variables (use throughout)

```css
:root {
  --bg-primary: #0a0a0f;
  --bg-card: #13131a;
  --bg-card-hover: #1a1a24;
  --border: rgba(255, 215, 0, 0.15);
  --gold: #FFD700;
  --gold-dim: #FFA500;
  --gold-glow: rgba(255, 215, 0, 0.3);
  --green: #22c55e;
  --red: #ef4444;
  --yellow: #eab308;
  --text-primary: #f0f0f0;
  --text-secondary: #a0a0b0;
  --text-muted: #606070;
  --font: 'Segoe UI', system-ui, -apple-system, sans-serif;
}
```

---

## Animation

Add on-load animation to all cards:

```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.indicator-card, .forecast-card, .exec-summary {
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
}

/* Stagger each card */
.indicator-card:nth-child(1) { animation-delay: 0.1s; }
.indicator-card:nth-child(2) { animation-delay: 0.2s; }
/* ... etc */
```
