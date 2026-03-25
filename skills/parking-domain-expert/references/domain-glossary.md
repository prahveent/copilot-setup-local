# Parking Domain Glossary

> Load this file when encountering an unfamiliar parking term, or when a user asks for a definition.

## Core Terms

| Term | Language | Definition |
|------|----------|------------|
| Kontrollanmerkelse | Norwegian | Private parking control fee (not a public fine; contractual claim) |
| Parkeringsforskriften | Norwegian | Detailed parking regulations under Parkeringsloven |
| Parkeringsloven | Norwegian | The Parking Act (2016) — core Norwegian parking law |
| Avgift | Norwegian/Danish | Fee / charge (context-dependent) |
| Parkeringsafgift | Danish | Parking fee / private control fee |
| Pysäköinninvalvontamaksu | Finnish | Private parking monitoring fee |
| Inkasso | Nordic | Debt collection (process of pursuing unpaid fines via collection agency) |
| Inkassoloven | Norwegian | The Debt Collection Act |
| ANPR | English | Automatic Number Plate Recognition — camera system reads plates. **Detection method only, not a parking model.** ANPR works within zone-based, bay-based, and other parking models equally. |
| LPR | English | License Plate Recognition — US/international term for ANPR |
| Parking Model | English | How parking rights are organised at a facility — defines the rules that apply. Examples: zone-based (rights tied to a geographic zone), bay-based (rights tied to a numbered bay), time-restricted, contract-reserved. **Independent of detection method.** |
| Detection Method | English | How a violation is discovered. Two options: ANPR (automated camera) or patrol (foot officer). Works within any parking model. Both produce the same control sanction entity referencing the same zone. |
| OCR | English | Optical Character Recognition — the algorithm reading plate text |
| Zone | English | A defined geographic area with specific parking rules and tariffs |
| Grace period | English | Mandatory window after ticket expiry before enforcement can act |
| Overstay | English | Vehicle remains in zone beyond permitted time |
| Session | English | A single parking event: entry → exit |
| Contract parking | English | Pre-agreed entitlement for a vehicle/person to park in a zone |
| Whitelist | English | List of plates exempt from normal enforcement (contracts, HC, etc.) |
| HC badge | English | Disabled parking permit (Handicap; from EU blue badge scheme) |
| Kontrollanmerkelse | Norwegian | Private control fee (see above) |
| Kontrollavgift | Norwegian (older) | Older term for private parking fine; largely replaced by kontrollanmerkelse |
| Parkeringsvakt | Norwegian | Parking attendant / enforcement officer |
| Beboerparkering | Norwegian | Resident parking — zone reserved for local residents |
| Tidsbegrenset parkering | Norwegian | Time-limited parking zone |
| Avgiftsparkering | Norwegian | Paid parking zone |
| EL-bil | Norwegian | Electric vehicle (EV) |
| Elbilprivilegier | Norwegian | EV privileges (free parking, reduced fees — being phased out in many areas) |
| Vipps | Norwegian | Norway's dominant mobile payment app (owned by DNB/SpareBank) |
| MobilePay | Nordic | Mobile payment app dominant in Denmark and Finland |
| Pivo | Finnish | Finnish mobile payment app |
| Namsmann | Norwegian | Enforcement court / bailiff for debt recovery |
| Inkassovarsel | Norwegian | Formal debt collection warning (required before sending to inkasso) |
| Parkeringsskive | Danish | Parking disc — analogue time-limit enforcement tool |
| Traficom | Finnish | Finnish Transport and Communications Agency (regulator) |
| SVV | Norwegian | Statens vegvesen — Norwegian Public Roads Administration (parking regulator) |
| Datatilsynet | Norwegian/Danish | Data Protection Authority |
| Tietosuojavaltuutettu | Finnish | Data Protection Ombudsman (Finland) |
| OCPP | English | Open Charge Point Protocol — EV charger communication standard |
| EHF | Norwegian | Elektronisk handelsformat — Norwegian e-invoice format (public sector) |
| Finvoice | Finnish | Finnish e-invoice format (public sector) |

## Feature-Specific Terms

| Term | Definition |
|------|------------|
| Entry event | ANPR or manual record of vehicle entering a zone. Either detection method (ANPR camera or patrol officer) can create this record — the parking model (zone-based etc.) is independent of how entry is recorded. |
| Exit event | ANPR or manual record of vehicle leaving a zone |
| Session match | Pairing an entry event with its corresponding exit event |
| Plate confidence | OCR confidence score for plate recognition (0–100%) |
| Evidence package | Set of photos, timestamps, and metadata required for an enforceable ticket |
| Appeal | Formal challenge by vehicle owner to a issued control fee |
| Escalation | Moving an unpaid fee to the next stage of the collection process |
| Rate lock | Fixing the price per hour at the moment a session begins |
| Occupancy | Ratio of used spaces to total capacity in a zone |
| Dynamic tariff | A pricing rule that changes based on occupancy, time, or demand |
| Discount code | A code or identifier that applies a rate reduction to a session |
| Prepaid session | Session paid in full at start, before exit |
| Pay-on-exit | Session payment processed at exit, based on actual duration |

## Abbreviations

| Abbreviation | Expansion |
|-------------|-----------|
| ANPR | Automatic Number Plate Recognition |
| LPR | License Plate Recognition |
| HC | Handicap (disabled badge) |
| EV | Electric Vehicle |
| NOK | Norwegian Krone |
| DKK | Danish Krone |
| EUR | Euro |
| SVV | Statens vegvesen |
| PII | Personally Identifiable Information |
| GDPR | General Data Protection Regulation |
| OCPP | Open Charge Point Protocol |
| EHF | Elektronisk handelsformat |
