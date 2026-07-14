# Block 7 | Resources (Commercial)

## Data sources

| Resource | Location | Refresh |
|----------|----------|---------|
| Verified analytics export | `data/analytics/` (broadcast reach, social, sentiment) | Weekly |
| Sponsor register | `data/sponsors.json` (contract IDs, tiers, renewal dates; no terms) | On change |
| Activation calendar | `data/activations/` | Weekly |
| Report templates | `templates/` (one per sponsor tier) | On brand update |
| Prospect research notes | `data/prospects/` | Per engagement |

## Knowledge bases

- Sponsor tier definitions and entitlements matrix.
- Historical report archive (what each sponsor received, when).
- Renewal negotiation timeline playbook.

## Tools

- Report generator (template merge with verified analytics).
- Prospect fit scorer (brand alignment, budget signal, category conflict check).
- Renewal risk monitor (engagement pattern flags).

## Technical requirements

- Analytics figures pulled from verified export only, per R-COM-2.
- Generated documents carry contract IDs, never commercial terms, per R-COM-1.
