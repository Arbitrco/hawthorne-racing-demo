# Block 9 | Request: Monthly Sponsor Report

## Request

Generate the monthly performance report for a named sponsor, ready for Commercial
Director review.

## Inputs

- Sponsor contract ID (from `data/sponsors.json`)
- Verified analytics export for the reporting period
- Activation calendar entries for the period
- The sponsor's tier template from `templates/`

## Steps

1. Pull the sponsor's tier and entitlements from the register by contract ID.
2. Extract period figures from the verified analytics export: broadcast exposure,
   social reach and engagement, sentiment, activation attendance.
3. Compare against the same period last season and against contract benchmarks
   where defined.
4. Draft in workspace voice (Block 6): executive summary, results by entitlement,
   activation highlights, forward look.
5. Flag any figure that underperforms benchmark, with a suggested framing that is
   honest without volunteering negotiation leverage.

## Output contract

- DOCX from the sponsor's tier template, plus a one-paragraph internal cover note
  flagging anything the Commercial Director should read before sending.
- Every figure traceable to the analytics export. No public estimates (R-COM-2).
- Contract terms never appear; contract ID only (R-COM-1).
- Footer: generation timestamp, data period, reviewing owner field.

## Rules in force

Global Block 8 plus R-COM-1 through R-COM-3. Human approval required before
anything leaves the building (global rule 3).
