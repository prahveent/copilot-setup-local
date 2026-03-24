# Memory Schema Reference

This file defines the JSON structure for `memory/knowledge-store.json`.

## Top-level structure

```json
{
  "version": "1.0",
  "last_compacted": "2025-03-24T00:00:00Z",
  "concepts": {},
  "features": {},
  "markets": {},
  "competitors": {}
}
```

---

## concepts namespace

Key: `concept_id` (snake_case, e.g. `grace_period_norway`)

```json
{
  "grace_period_norway": {
    "concept_id": "grace_period_norway",
    "name": "Grace Period (Norway)",
    "aliases": ["observation window", "grace window", "Parkeringsforskriften §28"],
    "summary": "Mandatory window after ticket expiry before a kontrollanmerkelse can be issued.",
    "key_points": [
      "Minimum 10 minutes in most Norwegian municipalities",
      "Required by Parkeringsforskriften §28",
      "Extended for HC (disabled) badge holders",
      "ANPR systems must store observed_at separately from issued_at"
    ],
    "technical_notes": "ANPR: compare first_seen_at vs session.valid_until; gap >= grace_period_minutes before allowing ticket creation. Must handle clock skew (NTP sync required on cameras).",
    "regulatory_refs": ["Parkeringsforskriften §28", "Parkeringsloven §30"],
    "market": "NO",
    "related_concepts": ["kontrollanmerkelse", "anpr_session_matching", "hc_exemption"],
    "user_verified": false,
    "last_updated": "2025-03-24T00:00:00Z",
    "source": "agent_generated"
  }
}
```

### Field definitions

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| `concept_id` | string | ✅ | snake_case, unique |
| `name` | string | ✅ | Human-readable |
| `aliases` | string[] | ✅ | For duplicate detection |
| `summary` | string | ✅ | 1–3 sentences, embeddable |
| `key_points` | string[] | ✅ | 3–7 bullets |
| `technical_notes` | string | | Implementation-relevant detail |
| `regulatory_refs` | string[] | | Law, section, article |
| `market` | string | ✅ | "NO" \| "DK" \| "FI" \| "ALL" |
| `related_concepts` | string[] | | Other concept_ids |
| `user_verified` | boolean | ✅ | Set true when user confirms accuracy |
| `last_updated` | ISO8601 | ✅ | |
| `source` | string | ✅ | "agent_generated" \| "user_provided" \| "web_search" |

---

## features namespace

Key: `feature_id` (snake_case, e.g. `dynamic_pricing`)

```json
{
  "dynamic_pricing": {
    "feature_id": "dynamic_pricing",
    "name": "Dynamic Zone Pricing",
    "summary": "Demand-based tariff adjustment per zone, locked at session entry.",
    "status": "analysed",
    "core_entities": [
      "PricingRule {zone_id, valid_from, valid_to, price_per_hour, rule_type, priority}",
      "OccupancySnapshot {zone_id, timestamp, capacity, occupied}",
      "ActiveSession {plate, zone_id, applied_rate, rate_locked_at}"
    ],
    "happy_path": [
      "Vehicle enters zone",
      "System evaluates active PricingRule for zone at entry time",
      "Rate locked on session (applied_rate)",
      "Signage/app displays locked rate",
      "Session closes with locked rate for billing"
    ],
    "edge_cases": [
      "Rate change mid-session — must use locked rate",
      "Multiple overlapping rules — priority ordering required",
      "ANPR vs app entry — rate must sync",
      "Pre-paid sessions — rate must be committed at purchase"
    ],
    "regulatory": {
      "NO": "Tariff must be displayed before commitment (Parkeringsloven §14)",
      "DK": "No mandate, best practice to align",
      "FI": "Municipal zones may have price caps"
    },
    "integrations": ["anpr", "signage_api", "payment_gateway", "mobile_app"],
    "top_risks": [
      "Retroactive repricing if rate-lock logic fails",
      "Stale occupancy data causing wrong price signal",
      "Overlapping pricing rules not resolved"
    ],
    "market": "ALL",
    "user_verified": false,
    "last_updated": "2025-03-24T00:00:00Z"
  }
}
```

---

## markets namespace

Key: `market_id` (e.g. `NO`, `DK`, `FI`)

```json
{
  "NO": {
    "market_id": "NO",
    "name": "Norway",
    "currency": "NOK",
    "primary_laws": [
      "Parkeringsloven (2016)",
      "Parkeringsforskriften",
      "Vegtrafikklov"
    ],
    "regulator": "Statens vegvesen (SVV)",
    "enforcement_type": "Private control fee (kontrollanmerkelse) — not public fine",
    "grace_period_minutes": 10,
    "appeal_deadline_days": 15,
    "max_control_fee_nok": 1000,
    "debt_collection_framework": "Inkassoloven",
    "key_facts": [
      "Operators must be approved by SVV",
      "Evidence package (photos + timestamps) mandatory for enforceable ticket",
      "HC exemptions apply across all zones",
      "EV charging integration increasingly expected"
    ],
    "last_updated": "2025-03-24T00:00:00Z"
  }
}
```

---

## competitors namespace

Key: `competitor_id` (slug, e.g. `easyparkflowbird`)

```json
{
  "easyparkflowbird": {
    "competitor_id": "easyparkflowbird",
    "name": "EasyPark / Flowbird",
    "type": "operator_and_software",
    "nordic_presence": "strong_NO_SE",
    "strengths": ["Consumer app scale", "Brand recognition", "Hardware integration"],
    "weaknesses": ["Enforcement integration is bolt-on", "Legacy software UX", "Slow feature iteration"],
    "key_products": ["EasyPark app", "Flowbird ANPR", "Flowbird pay station"],
    "nordic_market_share_estimate": "~35% Norway by volume",
    "watch_items": ["Potential EV charging integration announced Q1 2025"],
    "differentiation_opportunity": "Tight enforcement-to-payment audit trail; modern API-first architecture",
    "last_updated": "2025-03-24T00:00:00Z",
    "source": "agent_generated",
    "confidence": "medium"
  }
}
```

---

## Duplicate Detection Algorithm

Before creating a new entry, compute overlap score:

```
overlap_score = (matching_keywords / total_keywords_in_new_entry) * 100

matching_keywords = intersection of:
  - new entry's name words
  - new entry's aliases
  vs.
  - all existing entries' names + aliases (same namespace)

If overlap_score >= 70%:
  → DO NOT create new entry
  → Merge into existing: update key_points, technical_notes, last_updated
  → Add new phrasings to aliases[]
```

## Freshness Rules

| Age | Action |
|-----|--------|
| < 30 days | Use as-is |
| 30–90 days | Use with freshness caveat ("last verified ~N weeks ago") |
| > 90 days | Regenerate, update entry |
| `user_verified: true` | Never auto-expire; require user to explicitly update |
