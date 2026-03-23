---
name: sri-lanka-investment-report
description: Generates a comprehensive, professionally designed investment analysis report for Sri Lanka. Use this skill whenever a user asks to analyse, compare, or report on Sri Lankan investment options — including fixed deposits, unit trusts, money market funds, government securities (T-bills, T-bonds), CSE equities, REITs, gold, repos, or any combination thereof. Trigger on phrases like "Sri Lanka investment", "SL investment report", "compare FDs and unit trusts Sri Lanka", "investment options in Sri Lanka", "analyse LKR investments", "generate investment report", or any request involving Sri Lankan financial instruments. Always produce both an HTML report (primary) and a Word document (secondary) unless the user specifies only one format.
---

# Sri Lanka Investment Report Skill

Generates a polished, data-rich investment landscape report covering all major investment instruments available in Sri Lanka. Output: a standalone HTML report (preferred) and optionally a Word .docx file.

---

## Workflow

### Step 1 — Gather Current Data (Always Search First)

Before writing any report, search the web for up-to-date figures. Run these searches in parallel:

1. `Sri Lanka fixed deposit rates 2026 banks finance companies`
2. `Sri Lanka Treasury bill bond yield CBSL 2026`
3. `Sri Lanka CSE ASPI stock market performance 2026`
4. `Sri Lanka unit trust fund returns 2025 2026 CAL First Capital`
5. `Sri Lanka inflation GDP CBSL policy rate 2026`

Extract and note: current FD rates by institution, T-bill yields, ASPI level, key macro figures (inflation, policy rate, LKR/USD). If search is unavailable, use the reference data in `references/default-data.md` but note it may be stale.

### Step 2 — Determine Output Format

Ask the user (or infer from context):
- **HTML report** (default, rich interactive) — always produce unless user says otherwise
- **Word document (.docx)** — produce if user asks for "Word", "docx", "downloadable report", or "document"
- **Both** — produce both formats

### Step 3 — Generate HTML Report

Read `references/html-template-guide.md` for the design system, then build the HTML file.

**Required sections** (all must be present):
1. Fixed navigation bar with section links
2. Hero section with macro dashboard (key stats from search)
3. Instrument cards (one card per major instrument — see list below)
4. Master comparison table (all instruments, risk-ranked)
5. Investor profile allocation section (3 profiles: conservative / moderate / aggressive)
6. Risks & regulatory framework
7. Disclaimer footer

**Instruments to cover** (all of these, always):
- Fixed Deposits: government banks (BOC, NSB), commercial banks, finance companies
- Money Market Funds (CAL, First Capital, Namal)
- Unit Trust Funds: all 5 types (money market, income, balanced, high yield, equity)
- Government Securities: T-Bills, T-Bonds, Repo Agreements, SLDBs
- CSE Equities (direct stocks)
- REITs
- NSB special products (savings certificates etc.)
- Gold (physical)
- Corporate Debentures
- Cryptocurrency (with regulatory warning)

**Design requirements:**
- Use Google Fonts: Playfair Display (headings) + DM Sans (body) + DM Mono (stats/code)
- Dark hero with gold accent color (`#c8922a`)
- Risk-coded cards: very-low=green, low=teal, medium=gold, high=orange, very-high=crimson
- Animated card reveals on scroll (IntersectionObserver)
- Fully responsive, print-friendly
- Must include: risk pill badges, stat grids per card, sticky nav, macro band

**Output path:** `/mnt/user-data/outputs/SriLanka_Investment_Report.html`

### Step 4 — Generate Word Document (if requested)

Read the docx skill at `/mnt/skills/public/docx/SKILL.md`, then build a `.docx` version covering the same content.

Sections for Word doc:
1. Cover page (flag emoji, title, subtitle, instruments listed, date)
2. Executive summary
3. Macroeconomic context (table: 2023 vs 2025-26 key indicators)
4. One section per instrument group (FDs, MMFs, Unit Trusts, Govt Securities, CSE, REITs, Alternatives)
5. Master comparison table
6. Investor profile allocation tables (3 profiles)
7. Regulatory framework table
8. Key risks (bullet list)
9. Conclusion & recommendations
10. Disclaimer box

**Output path:** `/mnt/user-data/outputs/SriLanka_Investment_Report.docx`

Run validation: `python3 /mnt/skills/public/docx/scripts/office/validate.py /home/claude/SriLanka_Investment_Report.docx`

### Step 5 — Present Files

Use `present_files` to share completed outputs with the user.

---

## Key Data Reference (Update via search each run)

See `references/default-data.md` for fallback data if search is unavailable.

### Rate Conventions
- FD rates: Quoted as annual p.a., gross before 5% WHT
- T-Bill/Bond yields: Annual, no WHT (key selling point — always highlight)
- Unit trust returns: Indicative annual, historically based
- CSE returns: Highly variable — always note past performance caveat

### Tax Summary Table (always include)
| Instrument | Tax Treatment |
|---|---|
| Bank / Finance FDs | WHT 5% on interest |
| T-Bills & T-Bonds | No WHT — significant advantage |
| Unit Trust distributions | Favourable (handled at fund level) |
| CSE capital gains | Exempt |
| CSE dividends | 15% |
| REIT distributions | 15% |
| Gold gains | WHT applies |

---

## Risk Classification

Always classify instruments using this 5-level scale:

| Level | Label | Colour | Examples |
|---|---|---|---|
| 1 | Very Low | Green `#2e9e4f` | NSB savings, T-bills, Repos, MMFs |
| 2 | Low | Teal `#5aab6e` | Bank FDs, T-Bonds, income unit trusts |
| 3 | Medium | Gold `#c8922a` | Finance FDs, REITs, balanced funds, debentures |
| 4 | High | Orange `#d46a2a` | Equity funds, gold |
| 5 | Very High | Crimson `#8b1a1a` | Direct CSE stocks, crypto |

---

## Investor Profile Templates

### Conservative (Capital Preservation, 1–3 yr horizon)
- 40% Bank FDs (BOC/NSB)
- 35% Government T-Bills / T-Bonds
- 20% Money Market Fund
- 5% Income Unit Trust

### Moderate (Balanced Growth, 3–7 yr horizon)
- 25% Fixed Deposits (Banks + Finance)
- 25% Government Bonds
- 25% Income / Balanced Unit Trust
- 15% CSE Equities / Equity Unit Trust
- 10% REITs

### Aggressive (Wealth Accumulation, 7–15+ yr horizon)
- 50% CSE Direct Stocks / Equity Unit Trust
- 15% REITs
- 15% High Yield / Balanced Fund
- 10% Government Bonds
- 10% Money Market (liquidity reserve)

---

## Quality Checklist

Before presenting files, verify:
- [ ] All 10+ instrument categories covered
- [ ] Macro dashboard has at least 5 live/current data points
- [ ] Master comparison table has all instruments ranked low→high risk
- [ ] Three investor profiles with % allocations sum to 100%
- [ ] Disclaimer is present and prominent
- [ ] HTML is self-contained (no broken external dependencies except Google Fonts CDN)
- [ ] Word doc validated (if generated)
- [ ] Files saved to `/mnt/user-data/outputs/`
- [ ] `present_files` called with output paths

---

## Common Customisations

If user requests variations, adapt accordingly:
- **"Only fixed deposits"** → Focus section, still include brief comparison table
- **"For a foreign/NRI investor"** → Emphasise SLDBs, REIT repatriation rules, FX risk section
- **"Islamic/Halal investments"** → Highlight CAL Islamic MMF, Shariah-compliant instruments
- **"Update rates"** → Re-run web searches, regenerate with new figures
- **"Add charts"** → Use Chart.js in HTML for return/risk bar charts; add to existing report
