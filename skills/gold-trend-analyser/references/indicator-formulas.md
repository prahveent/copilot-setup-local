# Technical Indicator Reference

## RSI (Relative Strength Index, period=14)
```
RS = Average Gain / Average Loss  (over 14 periods)
RSI = 100 - (100 / (1 + RS))

Signal:
  RSI < 30  → Oversold / Bullish reversal signal
  RSI 30–50 → Mildly bearish
  RSI 50–70 → Mildly bullish
  RSI > 70  → Overbought / Bearish reversal signal
```

## MACD (12, 26, 9)
```
MACD Line   = EMA(12) - EMA(26)
Signal Line = EMA(9) of MACD Line
Histogram   = MACD Line - Signal Line

Signal:
  MACD > Signal Line → Bullish
  MACD < Signal Line → Bearish
  Histogram turning positive → Bullish momentum
  Histogram turning negative → Bearish momentum
```

## Moving Averages
```
50-day SMA  = Sum(Close, 50) / 50
200-day SMA = Sum(Close, 200) / 200

Golden Cross: 50-day crosses above 200-day → Strong Bullish
Death Cross:  50-day crosses below 200-day → Strong Bearish
Price > 200MA → Uptrend
Price < 200MA → Downtrend
```

## Bollinger Bands (20, 2)
```
Middle Band = 20-period SMA
Upper Band  = Middle + (2 × StdDev)
Lower Band  = Middle - (2 × StdDev)
%B = (Price - Lower) / (Upper - Lower)

Signal:
  Price near Upper Band → Overbought
  Price near Lower Band → Oversold
  Squeeze (bands narrow) → Volatility breakout imminent
```

## Stochastic Oscillator (14, 3)
```
%K = (Close - Lowest Low(14)) / (Highest High(14) - Lowest Low(14)) × 100
%D = 3-period SMA of %K

Signal:
  %K < 20     → Oversold / Bullish
  %K > 80     → Overbought / Bearish
  %K crosses above %D → Bullish signal
  %K crosses below %D → Bearish signal
```

## ATR (Average True Range, period=14)
```
TR = max(High-Low, |High-PrevClose|, |Low-PrevClose|)
ATR = EMA(14) of TR

For gold:
  ATR < $15/oz   → Low volatility
  ATR $15–$35/oz → Normal volatility
  ATR > $35/oz   → High volatility
```

## ADX (Average Directional Index, period=14)
```
ADX < 25  → No trend / ranging market
ADX 25–50 → Moderate trend
ADX > 50  → Strong trend
ADX rising → Trend strengthening
ADX falling → Trend weakening

+DI > -DI → Bullish trend
-DI > +DI → Bearish trend
```

---

## Estimation Guide (when live data unavailable)

If exact indicator values aren't found in searches, estimate from context:

| Situation | RSI Est | MACD Est | Notes |
|-----------|---------|----------|-------|
| Strong uptrend, near highs | 65–75 | Positive | Mark as estimated |
| Consolidating near ATH | 55–65 | Slightly pos | Mark as estimated |
| Pulling back from highs | 40–55 | Turning neg | Mark as estimated |
| Correcting 5–10% | 30–45 | Negative | Mark as estimated |
| Strongly oversold | 20–35 | Negative | Mark as estimated |

Always add `*` footnote: "* Estimated based on price action context. Verify with live data."
