# Market Context: Finland (FI)

> Load this file when answering any Finland-specific regulatory or operational question.

## Regulatory Framework

| Law / Rule | Scope |
|------------|-------|
| Tieliikennelaki | Road traffic law — public road parking |
| Laki yksityisistä pysäköintipalveluista | Private parking services act |
| Perintälaki | Debt collection law |
| GDPR (via Tietosuojalaki) | Data privacy |

## Key Operational Facts

- **Regulator:** Traficom (transport and communications authority) for public roads; municipal authorities for city zones
- **Enforcement type:** Private parking fee (`pysäköinninvalvontamaksu`) — contractual
- **Currency:** EUR
- **Max control fee:** Varies; private operators typically 60–80 EUR; municipal fines are fixed by law
- **Grace period:** Not uniformly mandated; best practice 10 minutes
- **Appeal deadline:** Typically 14 days
- **Evidence requirement:** Photo evidence + timestamps required to defend disputes

## Differences vs. Norway

| Aspect | Norway | Finland |
|--------|--------|---------|
| Currency | NOK | EUR |
| Regulator | SVV | Traficom + municipalities |
| Fee cap | 1,000 NOK | ~60–80 EUR private |
| Mobile payment | Vipps | MobilePayFI / Pivo |
| ANPR maturity | High | Moderate |
| Language complexity | Norwegian | Finnish + Swedish (bilingual) |

## Language Note

Finland is bilingual (Finnish + Swedish). Parking signage in bilingual municipalities must appear in both languages. Zone names may have Finnish and Swedish variants. This can affect UI localisation scope.

## Payment & Billing

- **MobilePay** (shared Nordic service) used in Finland
- **Pivo** — Finnish mobile payment, bank-backed
- Card and online banking (verkkopankki) common
- EUR invoicing standard

## Data & Privacy

- Tietosuojavaltuutettu (Office of the Data Protection Ombudsman) is the Finnish DPA
- Plate data = personal data under GDPR
- ANPR footage: 30-day retention standard

## ANPR Specifics

- Finnish plates: format `ABC-123` (3 letters + 3 digits) or `AB-1234`
- Electric vehicle plates: no special visual distinction — EV status determined by registration database lookup
- Confidence threshold: ~95% standard

## Regional Notes

- Helsinki metropolitan area: largest market; complex zone structures; tram infrastructure affects parking zones
- Tampere, Turku, Oulu: significant secondary markets
- Seasonal: heavy winter (ice, snow) — ANPR performance degrades; manual fallback important
- Public sector clients (municipalities) common — EHF or Finvoice (Finnish e-invoice format) required
