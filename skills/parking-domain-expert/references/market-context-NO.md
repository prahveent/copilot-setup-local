# Market Context: Norway (NO)

> Load this file when answering any Norway-specific regulatory or operational question.

## Regulatory Framework

| Law / Rule | Scope |
|------------|-------|
| Parkeringsloven (2016) | Core parking law — operator rights, consumer protection |
| Parkeringsforskriften | Detailed regulations — grace periods, fee limits, signage, evidence |
| Vegtrafikklov | Road traffic law — public road parking |
| Inkassoloven | Debt collection — regulates how unpaid fees can be pursued |
| GDPR (via Personopplysningsloven) | Data privacy — applies to plate data, CCTV, session records |

## Key Operational Facts

- **Regulator:** Statens vegvesen (SVV) — operators must be SVV-approved
- **Enforcement type:** Private control fee (`kontrollanmerkelse`) — contractual, not a public fine
- **Currency:** NOK
- **Max control fee:** 1,000 NOK (as of last update)
- **Grace period:** Minimum 10 minutes after expiry; some municipalities extend to 15 min
- **Appeal deadline:** 15 calendar days from ticket issue date
- **Evidence requirement:** Photos (entry + violation), timestamps, zone ID, plate, officer/camera ID
- **HC exemption:** Disabled badge holders — extended grace period, some free zones

## Enforcement Escalation Chain

```
Observation (ANPR or patrol)
  ↓ grace period elapsed
Kontrollanmerkelse issued
  ↓ 15 days unpaid
Reminder / inkassovarsel
  ↓ still unpaid
Debt collection agency (Inkasso)
  ↓ disputed / ignored
Namsmann (enforcement court) — last resort
```

## Payment & Billing

- Dominant payment methods: Vipps (most used), card, bank transfer
- Vipps integration is **expected** by Norwegian operators — not optional
- Invoice billing common for contract/corporate parking
- E-invoice (EHF format) required for public sector clients

## Data & Privacy

- Plate data = personal data under GDPR (Norway)
- ANPR footage retention: typically 30 days max; check with DPA (Datatilsynet) for zone specifics
- Must have a Data Processing Agreement (DPA) with ANPR camera vendors

## ANPR Specifics

- Norwegian plates: format `AB 12345` (2 letters + 5 digits)
- Electric vehicles: plates starting with `EL` or `EK` — may have different zone rules
- Temporary plates: `M-XXXXX` format — enforce with caution
- Confidence threshold: Operators typically require ≥95% OCR confidence before auto-issuing ticket

## Seasonal / Regional Notes

- Oslo: most complex zone regulations; dynamic pricing pilots underway
- Bergen, Trondheim, Stavanger: largest markets outside Oslo
- Rural municipalities: often simpler flat-rate zones, fewer ANPR installations
- Winter: snow/ice affects plate OCR — operators should have manual override fallback

## Upcoming / Watch

- Dynamic pricing mandate discussion in Oslo City Council (2025)
- EV charging integration incentives for parking operators
- SVV reviewing max control fee — possible increase under consultation
