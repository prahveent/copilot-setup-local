---
name: sri-lanka-investment-report
description: Generates a comprehensive, professionally designed investment analysis report for Sri Lanka. Use this skill whenever a user asks to analyse, compare, or report on Sri Lankan investment options — including fixed deposits, unit trusts, money market funds, government securities (T-bills, T-bonds), CSE equities, REITs, gold, repos, or any combination thereof. Trigger on phrases like "Sri Lanka investment", "SL investment report", "compare FDs and unit trusts Sri Lanka", "investment options in Sri Lanka", "analyse LKR investments", "generate investment report", "unit trust guide Sri Lanka", "combine investment report", or any request involving Sri Lankan financial instruments. Always produce a single combined HTML file as the default output, plus a Word document if requested.
---

# Sri Lanka Investment Report Skill

Generates a single polished, data-rich combined HTML file containing both the full investment landscape report AND the unit trust deep-dive in one self-contained file with tab-based navigation. Optionally also produces a Word .docx file.

**Default output (single combined file):**
- `SriLanka_Complete_Investment_Guide.html` — One self-contained HTML file with two tab-switchable views:
  - **Tab 1 "Full Report"**: macro dashboard, all instruments, expanded unit trust section, master comparison table, investor profiles, risks & regulatory framework
  - **Tab 2 "Unit Trust Deep-Dive"**: how it works, all 9 fund types with named fund cards, fund manager table, comparison table, decision framework, how-to-invest steps

---

## Workflow

### Step 1 — Gather Current Data (Always Search First)

Before writing any report, search the web for up-to-date figures. Run these searches:

1. `Sri Lanka fixed deposit rates 2026 banks finance companies`
2. `Sri Lanka Treasury bill bond yield CBSL 2026`
3. `Sri Lanka CSE ASPI stock market performance 2026`
4. `Sri Lanka unit trust fund managers SEC registered 2025 2026`
5. `Sri Lanka inflation GDP CBSL policy rate 2026`

Extract and note: FD rates by institution, T-bill yields, ASPI level, key macro figures (inflation, policy rate, LKR/USD), unit trust fund performance data. If search is unavailable, use `references/default-data.md` but note figures may be stale.

### Step 2 — Determine Output Format

Infer from context:
- **Single combined HTML** (default) — always produce `SriLanka_Complete_Investment_Guide.html` unless user says otherwise
- **Word document (.docx)** — add if user asks for "Word", "docx", "downloadable", or "document"
- **Separate files** — only produce `SriLanka_Investment_Report.html` + `SriLanka_UnitTrust_Guide.html` separately if user explicitly asks for "separate files" or "two files"

### Step 3 — Generate Combined HTML (`SriLanka_Complete_Investment_Guide.html`)

Read `references/html-template-guide.md` for the design system. Build a **single self-contained HTML file** with two tab-switchable views navigated via a sticky top nav.

**Navigation structure:**
```html
<nav>
  [Brand] | [Tab: 📊 Full Report] | [Tab: 🏦 Unit Trust Deep-Dive] | [Context nav links]
</nav>
```
- Clicking a tab switches between `<div id="view-main">` and `<div id="view-ut">` using `display:none/block`
- Context nav links update dynamically to match the active tab's sections
- Clicking "Open Unit Trust Tab" button inside the main report switches to the UT tab

**View 1 — Full Report (`id="view-main"`):**

Required sections:
1. Hero with live macro badges (OPR, inflation, ASPI, reserves, GDP, LKR)
2. Macro dashboard band (6 metric tiles, dark slate background)
3. Executive summary with risk matrix (5 levels)
4. Instruments section: FDs, Govt. Securities, CSE Equities, REITs & Alternatives (cards with colour-coded top stripe)
5. Unit Trust Summary section with filter buttons + card grid + "switch to UT tab" CTA button
6. Master comparison table (all 19 instruments low→high risk)
7. Investor profiles (3 cards: conservative / moderate / aggressive)
8. Key Risks + Regulatory Framework table
9. Disclaimer
10. Footer

**View 2 — Unit Trust Deep-Dive (`id="view-ut"`):**

Required sections:
1. UT hero (teal/navy gradient, stat badges, live OPR notice)
2. How It Works: 4-step flow (Investor → AMC → Trustee Bank → SEC) + pros/cons side-by-side grid
3. All fund types with filterable card grid (filter: All/Money Market/Income/Gilt Edged/High Yield/Balanced/Equity/Shariah/Closed-End/Sector). Include all named funds from `references/unit-trust-funds.md`
4. Licensed Fund Managers table (10 major AMCs)
5. Fund Type Comparison table (all 9 types)
6. Decision Framework (5 questions with colour-coded answer pills) + How-to-Invest 5-step flow
7. Disclaimer
8. Footer (same as main)

**Unified JS functions required:**
```javascript
function switchTab(name)  // switches active view, updates context nav links, scrolls to top, re-triggers animations
function filterUT(type, btn)  // filters #utGrid cards by data-ut attribute (main report)
function ff(type, btn)    // filters #fg fund cards by data-t attribute (UT deep-dive)
function triggerVisible() // IntersectionObserver scroll animations for .card and .fc elements
```

**Design system (from `references/html-template-guide.md`):**
- Main report uses Playfair Display + DM Sans + DM Mono
- UT deep-dive uses Cormorant Garamond + Outfit + JetBrains Mono
- Both share the same CSS custom properties (unified :root)
- Fund cards use colour-coded top stripes (main) or themed headers (UT deep-dive)
- All cards animate in on scroll via IntersectionObserver

**Output:** `/mnt/user-data/outputs/SriLanka_Complete_Investment_Guide.html`

### Step 5 — Generate Word Document (if requested)

Read `/mnt/skills/public/docx/SKILL.md`, then build `.docx` covering both report sections as chapters:
1. Cover page
2. Executive summary + macro context table
3. All instrument groups (FDs, Govt Securities, CSE, REITs, Alternatives)
4. Full unit trust chapter: all 9 types + named fund examples per type
5. Master comparison table
6. Investor profile tables (3 profiles)
7. Regulatory framework table
8. Key risks
9. Conclusion & recommendations
10. Disclaimer box

**Output:** `/mnt/user-data/outputs/SriLanka_Complete_Investment_Guide.docx`
Validate: `python3 /mnt/skills/public/docx/scripts/office/validate.py /home/claude/SriLanka_Complete_Investment_Guide.docx`

### Step 6 — Present Files

Use `present_files` to share all completed outputs. Present HTML file first.

---

## Key Data Reference

See `references/default-data.md` for fallback figures.
See `references/unit-trust-funds.md` for complete unit trust fund details.
See `references/html-template-guide.md` for design system.

### Rate Conventions
- FD rates: Annual p.a., gross before 5% WHT
- T-Bill/Bond yields: Annual, **no WHT** — always highlight this advantage
- Unit trust returns: Indicative annual, historically based — always add past-performance caveat
- CSE returns: Highly variable — note capital gains are tax exempt

### Tax Summary (always include)
| Instrument | Tax on Income | Capital Gains |
|---|---|---|
| Bank / Finance FDs | WHT 5% | N/A |
| T-Bills & T-Bonds | **No WHT** | N/A |
| Unit Trust distributions | Favourable | Generally exempt |
| CSE shares | 15% dividend tax | **Exempt** |
| REITs | 15% on distribution | Subject to CGT |
| Gold | WHT on gains | Applies |
| Crypto | Unclear / evolving | Unclear |

---

## Risk Classification (5-level — use consistently)

| Level | Label | Colour | Examples |
|---|---|---|---|
| 1 | Very Low | Green `#2e9e4f` | NSB savings, T-bills, Repos, MMFs, Gilt Edged UTs |
| 2 | Low | Teal `#5aab6e` | Bank FDs, T-Bonds, income/bond UTs, closed-end |
| 3 | Medium | Gold `#c8922a` | Finance FDs, REITs, balanced funds, debentures |
| 4 | High | Orange `#d46a2a` | Equity funds, high yield, gold, sector funds |
| 5 | Very High | Crimson `#8b1a1a` | Direct CSE stocks, crypto |

---

## Investor Profile Templates

### Conservative (1–3 yr): 40% Bank FDs · 35% T-Bills/T-Bonds · 20% MMF · 5% Income UT
### Moderate (3–7 yr): 25% FDs · 25% T-Bonds · 25% Income/Balanced UT · 15% Equities/Equity UT · 10% REITs
### Aggressive (7–15+ yr): 50% CSE/Equity UT · 15% REITs · 15% High Yield/Balanced UT · 10% T-Bonds · 10% MMF

---

## Quality Checklist

Before presenting, verify:
- [ ] Single combined HTML file generated (`SriLanka_Complete_Investment_Guide.html`)
- [ ] Tab switching works (Full Report ↔ Unit Trust Deep-Dive)
- [ ] Context nav links update when switching tabs
- [ ] Macro dashboard has 6 live data points
- [ ] Main report: all 10+ instruments covered with cards
- [ ] Main report: UT section has filter buttons + 9+ fund cards + "switch tab" CTA
- [ ] Master comparison table has 19 instruments ranked low→high risk
- [ ] 3 investor profiles sum to 100%
- [ ] UT deep-dive: all 9 fund types with named fund cards (20+ cards total)
- [ ] UT deep-dive: fund manager table with 10+ AMCs
- [ ] UT deep-dive: decision framework with 5 questions
- [ ] UT deep-dive: 5-step how-to-invest flow
- [ ] Disclaimers present in both views
- [ ] HTML is fully self-contained (Google Fonts CDN only external)
- [ ] Scroll animations work on card/fc elements in both views
- [ ] Word doc validated if generated
- [ ] All files in `/mnt/user-data/outputs/`
- [ ] `present_files` called

---

## Common Customisations

- **"Only fixed deposits"** → Focus FD section + brief comparison table
- **"For a foreign/NRI investor"** → Emphasise SLDBs, REIT repatriation, FX risk
- **"Islamic/Halal"** → Highlight CAL Islamic MMF + Senfin Shariah Income Fund prominently
- **"Update rates"** → Re-run web searches, regenerate with fresh figures
- **"Add charts"** → Use Chart.js CDN for return/risk bar charts in HTML
- **"Separate files"** → Generate `SriLanka_Investment_Report.html` + `SriLanka_UnitTrust_Guide.html` separately instead of combined file
- **"Just unit trusts"** → Extract and generate only the UT deep-dive view as a standalone file
