# Block 7 | Resources (Race Operations)

## Data sources

| Resource | Location | Refresh |
|----------|----------|---------|
| Meeting transcripts | `data/transcripts/` (race weekend + factory strategy meetings) | Per meeting |
| Decision ledger | `data/decision-ledger.json` | Per analysis run |
| Tyre model summaries | Strategy team export, `data/tyre-models/` | Per event |
| Timing data extracts | `data/timing/` (sanitised, no rival confidential data) | Per session |
| Regulation summaries | `data/regs/` (sporting reg digests, human-verified) | Per FIA update |

## Knowledge bases

- Decision method taxonomy: consensus, consultative, delegated, directive, escalated.
- Bias taxonomy: 71 patterns across cognitive, group dynamic, and structural categories.
- Historical ledger: every tracked decision since programme start, with outcomes
  where known.

## Tools

- Transcript processor (speaker attribution, decision extraction).
- Ledger maintainer (append-only writes, schema-validated).
- Brief generator (Situation/Options/Watch-outs template).

## Technical requirements

- All processing on team infrastructure per global rule 1.
- Ledger writes are append-only; corrections are new entries referencing the original.
