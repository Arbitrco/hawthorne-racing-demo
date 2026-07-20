---
name: content-idea-scan
description: Gather fan-facing and sponsor-activation content ideas from changes anywhere in the Hawthorne Racing Cortex. Trigger when the user asks to find, gather, or scan for content ideas, social post ideas, or things to post about. Scans git changes repo-wide across every folder — global, all workspaces including race operations, and any future ones — plus a derived-dates layer (upcoming activation windows, partnership anniversaries, founding anniversary, race weekends). Surfaces only publicly shareable signals and excludes by content type wherever it appears: technical IP, Tier 1 sponsor terms, Tier 2 race strategy, regulatory interpretation, and personnel matters never surface, and 03-personal/ is never read. Writes a rolling backlog at 02-workspaces/01-commercial/05-deliverables/content-ideas-backlog.md and hands selected ideas to a named human for scheduling. All drafted copy is marked [REVIEW] and follows the Commercial Block 6 voice.
---

# Skill: Content Idea Scan

## Purpose

Turn changes anywhere in the Hawthorne Racing Cortex into a working list of
fan-facing and sponsor-activation content ideas. The Cortex is a git repository, so
most things worth talking about show up as commits (a new sponsor or partner, a new
or expanded activation, a publicly shareable milestone, a race result, a new
fan-facing offering). Upcoming windows and anniversaries are derived from data
already in the repo. This skill reads both, drafts the publicly promotable ones as
content ideas, and maintains a single rolling backlog the Commercial team works from.

### Scope: whole repo, filtered by content not by folder

The scan reads changes across **every folder in the repo** — `01-global/`, both
current workspaces (Commercial and Race Operations), and **any workspace added in
future** — so no publicly shareable signal is missed just because of where it lives.
A race result or a podium recorded in Race Operations is legitimate fan content.

What keeps this safe is not a folder allow-list but a **content filter applied
everywhere**: only publicly shareable material is surfaced, and confidential
material is excluded by type wherever it appears. Because the filter is
content-based, new workspaces are covered automatically with no edit to this skill.

Two boundaries are absolute and are never crossed for any folder, present or future:

1. **`03-personal/` is never read** — private, gitignored, hard exclusion (below).
2. **Tier 2 / IP content types are never opened or surfaced** — race strategy,
   decision ledgers, meeting transcripts, tyre and timing and simulation data, and
   any technical IP. You may see their paths in `git diff --name-only`; do not read
   their diffs and never place their content in the backlog (global Rule 8
   confidentiality tiers, R-OPS-1, R-COM-3). Reading a path list to exclude a file
   is not the same as summarising Tier 2 data into a commercial output — the latter
   never happens.

This skill covers change-driven and date-derived ideas. The activation calendar
(`03-data/activations/`) and the season race calendar are the scheduling backbone
that decides *when* an idea runs. This skill decides *what* is worth running.

## When to use

Use when the user asks to find, gather, or scan for content ideas, social post
ideas, or "things to post about". This is a Commercial-owned skill: it scans the
whole repo but produces external, fan-facing and sponsor-facing content, so the
Commercial Block 6 voice applies to every drafted line and the output is a
Commercial deliverable.

## Output

A single rolling backlog at
`02-workspaces/01-commercial/05-deliverables/content-ideas-backlog.md`. The skill
appends new open ideas, regenerates the upcoming-dates section, and updates the
baseline marker on every run. It never creates dated per-run files.

---

## Hard exclusion — the `03-personal/` workspace

`03-personal/` is private, gitignored, never synced, and must never be indexed or
used. This is an absolute rule that applies to every mode of this skill
(incremental git scan, full-content sweep, or any subagent you dispatch). It
overrides everything else.

- **Never read, open, `cat`, grep, or glob any path under `03-personal/`.** Not
  for inspection, not "just to check".
- **Never pass a `03-personal/` path to any tool, command, or subagent**, and
  never include it in a file list you hand off.
- **If you dispatch a subagent** (for example to sweep the repo for promotable
  material), the dispatch instructions must state explicitly that `03-personal/`
  is out of bounds, and you must build the file list with `03-personal/` already
  removed before sending it.
- **For a full-content sweep** (treating all current docs as new), exclude
  `03-personal/` when enumerating files, before any read. The git path is safe
  because `03-personal/` is gitignored, but full-content reads are not — this is
  where the rule matters most.
- **Never use content that originated from `03-personal/`**, even if it reaches
  you some other way. If you notice `03-personal/`-sourced material in a result,
  drop it and tell the user it was excluded.

When in doubt, treat anything under `03-personal/` as if it does not exist.

---

## Step 1 — Resolve the baseline

Read `02-workspaces/01-commercial/05-deliverables/content-ideas-backlog.md` and
take `scanned_to_commit` from the frontmatter. This is where the last run stopped.

- If the file exists and has a valid `scanned_to_commit`, that SHA is the baseline.
- If the file does not exist, or the marker is missing, fall back to "changes in
  the last 30 days" and state this assumption clearly in the run summary. Create
  the backlog file in Step 6 using the format below.
- If the recorded commit cannot be found in history (history was rewritten), fall
  back to the last 30 days and warn the user.

Confirm the current HEAD: `git rev-parse HEAD`. This becomes the new
`scanned_to_commit` once the run completes.

If git is not available or this is not a git repository, stop and tell the user.
Do not guess at changes.

## Step 2 — Collect git changes

Get the commits and the full, repo-wide list of changed files since the baseline.
Do not filter by path at this stage — the scan covers every folder so future
workspaces are picked up with no edit to this skill.

```
git log <baseline>..HEAD --pretty=format:"%h %ad %s" --date=short
git diff <baseline>..HEAD --name-only
```

(When falling back to a time window, use `git log --since="30 days ago"` and
`git diff` against the commit closest to 30 days ago.)

### Triage the changed-file list into three lanes

Sort every changed path into one of three lanes **before reading any diff**:

**Lane A — public-eligible (read the diff, extract specifics).** Anything that can
hold publicly shareable material, in any folder. High-signal examples:

- `02-workspaces/01-commercial/03-data/sponsors.json` — new sponsor/partner rows
  (contract ID, tier, dates — never terms)
- `02-workspaces/01-commercial/03-data/activations/` — new or expanded activations
- `01-global/01-context/2-company.md` — awards, values, milestones, roster
  additions, publicly shareable achievements
- `01-global/01-context/3-products-services.md` — new or expanded fan-facing offerings
- `01-global/01-context/4-context.md` — publicly known season position and milestones
- `02-workspaces/01-commercial/03-data/analytics/` — verified, publicly shareable
  reach milestones only (R-COM-2)
- **Race Operations public results** — already-broadcast facts only: finishing
  positions, podiums, points, poles, fastest laps, championship position. A
  results or race-report file under Race Operations that carries only public
  outcomes is Lane A. If a file mixes public results with strategy, treat it as
  Lane B and do not read it.
- Any file in a **future workspace** that holds announced, public-facing material.

**Lane B — Tier 2 / IP restricted (do NOT read the diff, never surface).** Excluded
by content type wherever the path lives, now or in future:

- Race strategy, `decision-ledger.json`, meeting transcripts, tyre models, timing
  extracts, simulation data, any aerodynamic or design or technical IP
  (global Rule 8 tiers, R-OPS-1, R-COM-3, global Rule 1).
- Sponsor commercial terms / contract value (Tier 1, R-COM-1).

You may see Lane B paths in `--name-only`; that is fine. Do not open them, and never
place their content in the backlog. Reading a path list is not summarising Tier 2.

**Lane C — hard exclusion (`03-personal/`).** Never read or pass any path, in any
mode — see the Hard exclusion section above. It is gitignored so it should not
appear in git output anyway.

Then pull diffs for Lane A files only, for example:

```
git diff <baseline>..HEAD -- 02-workspaces/01-commercial/03-data/sponsors.json
git diff <baseline>..HEAD -- 01-global/01-context/2-company.md
```

If there are no changes since the baseline, continue anyway — Step 4 still produces
upcoming dates. Report "no new git changes since last run" in the summary.

## Step 3 — Classify each change

Sort every change into one of two buckets. Surface only the publicly promotable
ones. When in doubt, exclude.

### Promotable (becomes a content idea)

| Signal | Source | Idea type |
|---|---|---|
| New sponsor or partner row (public announcement, contract ID only) | `03-data/sponsors.json` | Partnership announcement (with sponsor sign-off check) |
| New or expanded activation | `03-data/activations/` | Activation / fan-event promo |
| New award, value, milestone, or publicly known season position | `2-company.md`, `4-context.md` | Company or season milestone |
| New or expanded fan-facing offering | `3-products-services.md` | Content, community, or merchandise launch |
| Verified, publicly shareable reach milestone | `03-data/analytics/` | Audience milestone (figure per R-COM-2) |
| Public race result: podium, points, pole, fastest lap, championship move | Race Operations (Lane A results only) | Race-result / fan celebration post |
| Announced, public-facing change in a future workspace | any new workspace | As fits the change type |

### Exclude from the backlog (do not surface)

Exclusion is by **content type, wherever it appears** — global, Commercial, Race
Operations, or any future workspace. Do not list excluded material anywhere in the
backlog. These enforce global Block 8 and the Commercial extensions R-COM-1–3:

- **Technical IP** — aerodynamic data, design geometry, simulation source or
  output. Never promotable, in any folder (global Rule 1).
- **Tier 1 sponsor commercial terms** — contract value, discounts, entitlement
  pricing. Reference sponsors by contract ID only, never terms (R-COM-1).
- **Tier 2 race strategy data** — strategy calls, decision ledgers, meeting
  analysis, tyre and timing detail, and any strategy beyond what is already public
  (global Rule 8 tiers, R-OPS-1, R-COM-3). These are Lane B: not read, not surfaced.
  Note the boundary is the *content type*, not the folder — a **public race result**
  from Race Operations is promotable (Lane A); the strategy behind it is not.
- **Regulatory interpretation** — never draft anything that reads as advice on FIA
  compliance (global Rule 2).
- **Rival teams' confidential information** — never speculate on or reference it.
- **Personnel matters** — never a public post that evaluates an individual driver
  or staff member, and never announce a departure (global Rule 4). A factual roster
  addition (new hire, with consent) is promotable; a judgement or a departure is not.
- Any unverified or public-estimate figure (R-COM-2 requires the verified analytics
  export).

If a change looks like it could be a future story but is not yet promotable (for
example a partnership signed but not cleared for announcement, or an activation
still in planning), do not list it in the backlog. Mention it once in the run
summary to the user instead, then let it go.

## Step 4 — Compute derived dates

These are not git changes. Read `03-data/activations/`, `03-data/sponsors.json`,
`01-global/01-context/2-company.md`, and the race calendar (see below).

- **Upcoming activation windows** — from `03-data/activations/`, surface any
  activation whose window opens within the horizon (default 45 days from today).
- **Partnership anniversaries** — from `sponsors.json` start dates, compute the
  next anniversary of each active partnership. Include it if it falls within the
  window. Mark round-number milestones (1, 3, 5, 10+ years) as higher value.
- **Company founding anniversary** — founded February 2010 (`2-company.md`). Surface
  the February anniversary when it falls in the window; round-number years are
  higher value.
- **Staff work anniversaries** — the roster in `2-company.md` carries `Started`
  dates. Surface round-number tenure anniversaries in the window as optional
  people-content, each with a consent check. Never frame as a performance judgement
  (global Rule 4).
- **Season race weekends** — read the global race calendar at
  `01-global/03-data/race-calendar-2026.md` (public data, shared by all workspaces).
  Surface upcoming home-race (British GP, Silverstone) and marquee weekends in the
  window as fan-hype windows. If the file is missing, add a "confirm race-calendar
  source" note rather than inventing dates.
- This section is regenerated on every run, not appended to, because it is
  forward-looking.

## Step 5 — Generate ideas

Turn each promotable signal and each upcoming date into an idea entry with:

- **Trigger** — what changed or what is coming, with the date and source (e.g. "New
  row in sponsors.json — [partner], [tier], contract [ID], announced [date]")
- **Angle** — the marketing hook. Sponsor's outcomes first, team achievement second,
  per the Block 6 voice. Audience-aware per the Block 1 workspace extension (fans,
  and sponsor-side CMOs and partnership managers).
- **Channel** — default LinkedIn for sponsor-facing, primary social for fan-facing,
  until an active-channels list is added to the workspace resources.
- **Sign-off check** — for any idea featuring a sponsor: "Confirm [partner] has
  approved this announcement before posting" (R-COM-1, global Rule 3). For any idea
  featuring an individual: "Confirm [name] is happy to be featured before posting"
  (global Rule 4).
- **Draft hook** — one or two lines following `01-context/6-voice.md`: warm-
  professional, no em dashes, no excitement clichés (thrilled, delighted, game-
  changer), and no superlative without a number attached. Marked `**[REVIEW]**`.

Keep draft hooks short. They are starters for a human, not finished posts.

## Step 6 — Write or update the backlog

Dedupe first: before appending, check existing open and archived ideas. Match on
signal type + subject + occurrence date so the same signal is not added twice, and
a recurring anniversary is added once per occurrence.

Then:

1. Append genuinely new ideas to **Open ideas**, each with a new sequential ID
   (`IDEA-NNN`, from `next_idea_number`), status `New`, and the found date and commit.
2. Regenerate the **Upcoming windows and milestones** section for the current window.
3. Update frontmatter: `scanned_to_commit` to current HEAD, `last_scanned` to today,
   and `next_idea_number`.

Do not write a "not for public posting" section. Technical, strategic,
commercial-sensitive, and personnel changes are excluded from the backlog entirely.

### Backlog file format

```markdown
---
doc_type: backlog
workspace: commercial
parent: 02-workspaces/01-commercial/CLAUDE.md
reviewing_owner: Commercial Director
scanned_to_commit: <full SHA of HEAD at last run>
last_scanned: 2026-07-20
next_idea_number: 10
---

# Content Ideas Backlog

## Open ideas

### [IDEA-009] Partnership announcement — [Partner] (Associate Partner)
- **Status:** New
- **Found:** 2026-07-20 (commit abc1234)
- **Trigger:** New row in sponsors.json — [Partner], Associate Partner, contract HRC-0142, announcement cleared 2026-07-18
- **Angle:** Welcome the partner; frame the reach and audience they now stand in front of, their outcome first
- **Channel:** LinkedIn + primary social
- **Sign-off check:** Confirm [Partner] has approved this announcement before posting
- **Draft hook:** [one or two lines] **[REVIEW]**

## Upcoming windows and milestones
*Regenerated each run. Window: next 45 days as of 2026-07-20.*

- 2026-08-02 — Activation window opens: [activation name] (from 03-data/activations/)
- 2026-08-15 — [Partner] partnership, 3 years (contract HRC-0098)
- 2026-08-21 — Round 14, Dutch GP (Zandvoort), sprint weekend (race-calendar-2026.md)
- 2027-02 — Company founding anniversary, 17 years (founded Feb 2010)

## Archive

### [IDEA-003] ... — Status: Handed off (2026-06-20)

## Related

- 02-workspaces/01-commercial/CLAUDE.md — Commercial workspace manifest
- 02-workspaces/01-commercial/01-context/6-voice.md — Block 6 voice
- 02-workspaces/01-commercial/01-context/7-resources.md — data sources
- 02-workspaces/01-commercial/03-data/activations/ — activation calendar
- 01-global/03-data/race-calendar-2026.md — season race weekends (global, public)
```

**Status lifecycle:** `New` → `Handed off` → `Posted`, or `Dismissed`. Move Posted
and Dismissed ideas to **Archive** to keep the open list clean. IDs are never reused.

## Step 7 — Hand off for scheduling

Only after the user has seen the new open ideas and chosen which to take forward.

Nothing in this repo posts automatically. No social or publishing MCP is currently
configured (`.mcp.json` `mcpServers` is empty), and global Rule 3 requires a named
human to approve anything that leaves the building. So the backlog is the handoff
artifact:

1. Confirm with the user which ideas to advance and to which channel.
2. Mark each selected idea `Handed off` in the backlog, with the target channel and
   the reviewing owner (default Commercial Director).
3. Confirm every sponsor idea has its sign-off check satisfied before handoff, and
   every idea featuring an individual has consent confirmed.

If a publishing or social MCP is later added under `mcpServers` in `.mcp.json`, this
step may push selected ideas as drafts only (never scheduled or published), and set
their status to `Handed off`. Never post automatically, in any mode.

---

## Guardrails

- The scan reads the whole repo (all folders, all workspaces, current and future),
  but exclusion is by content type wherever it appears: technical IP, Tier 1 sponsor
  terms, Tier 2 race strategy, and personnel judgements never appear in the backlog.
  They are excluded, not flagged or listed.
- Two boundaries are absolute for every folder, present or future: `03-personal/` is
  never read (Lane C), and Tier 2 / IP content types are never opened or surfaced
  (Lane B). Public race results from Race Operations are in scope (Lane A); the
  strategy behind them is not.
- Sponsor sign-off on every partnership idea, and consent on every idea featuring an
  individual, before it can be handed off.
- Nothing posts automatically. A named human reviews and approves everything before
  publishing (global Rule 3).
- Fan-and-sponsor audience, outcome-first angles per the Block 1 workspace
  extension, and all drafted copy follows `01-context/6-voice.md` including the
  em-dash and excitement-cliché rules. Mark all drafted copy `**[REVIEW]**`.
- Every audience or reach figure is traceable to the verified analytics export
  (R-COM-2). No public estimates, no interpolated statistics.

## Error handling

| Case | Behaviour |
|---|---|
| No prior baseline marker | Fall back to last 30 days; state the assumption |
| Baseline commit not found | Fall back to last 30 days; warn the user |
| Not a git repo / git unavailable | Stop with a clear message; do not guess |
| No git changes since last run | Still regenerate upcoming dates; report "no new changes" |
| Duplicate signal on re-run | Dedupe against open and archived ideas |
| Recurring anniversary | Added once per occurrence |
| Staff or driver departure | Excluded; never a public idea (global Rule 4) |
| Sponsor announcement not yet cleared | Excluded; mention once in run summary, do not list |
| New / unknown workspace folder appears | In scope automatically; triage by content type (Lane A/B), never by folder name |
| Lane B path (strategy, ledger, transcript, IP) in the diff | Do not read the diff; do not surface. Seeing the path is fine |
| File mixes public results with strategy | Treat as Lane B; do not read. Only clearly public-outcome files are Lane A |
| No publishing MCP configured | Backlog is the handoff; a named human takes it forward |

## House conventions

- Plain-markdown backlog with a lightweight frontmatter marker (`scanned_to_commit`,
  `last_scanned`, `next_idea_number`) and a `## Related` section of relative paths.
- `[REVIEW]` markers on all drafted narrative.
- Follow `01-context/6-voice.md` for every drafted hook.
- Reviewing owner defaults to the Commercial Director, per the workspace role.
