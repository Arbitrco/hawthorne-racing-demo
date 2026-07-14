# Block 9 | Request: Meeting Decision Analysis

The execution lever. Run this against any strategy or debrief transcript.

## Request

Analyse the supplied meeting transcript and produce a decision intelligence report.

## Inputs

- Transcript file from `data/transcripts/`
- Current decision ledger from `data/decision-ledger.json`
- Current `decision-log.md`

## Steps

1. Extract every decision: explicit calls, implicit commitments, and deferred items.
2. For each decision, identify: owner, method used, evidence cited, deadline, and
   reversibility.
3. Screen the discussion against the bias taxonomy. Flag patterns with transcript
   line references as evidence.
4. Cross-reference the ledger: link related prior decisions, flag contradictions
   with earlier calls, update status of previously open items.
5. Append new entries to the ledger.
6. Append a matching row per decision to `decision-log.md` (next unused `#`,
   never renumbered), so the human-readable log stays in sync with the ledger.
7. Generate the report in workspace voice (Block 6): Situation, Options
   considered, Decisions made, Bias flags, Open items.

## Output contract

- One-page report per Block 6 conventions, plus ledger diff and
  `decision-log.md` diff.
- Every claim cites transcript lines. Every bias flag names the pattern, not a person.
- Report footer: generation timestamp, source file, reviewing owner field (blank
  for human completion).

## Rules in force

Global Block 8 plus R-OPS-1 through R-OPS-3. In particular: Tier 2 confidentiality,
no personnel judgements, recommendations are inputs not decisions.
