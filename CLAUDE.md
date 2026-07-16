# Hawthorne Racing | Project Instructions

This file is loaded automatically at the start of every Claude Code session
in this repo. It is the root manifest for the Hawthorne Racing AI Brain: it
maps the workspace to the nine blocks of the AI Strategy Canvas, defines
what loads globally versus what loads per workspace, and sets the standing
rules for the session.

## Load instruction (session start)

The following are loaded automatically as part of this file being read.
No manual step is required for these:

- `01-global/01-context/1-target-audience.md`
- `01-global/01-context/2-company.md`
- `01-global/01-context/3-products-services.md`
- `01-global/01-context/4-context.md`
- `01-global/01-context/8-rules.md`

Blocks 5, 6, 7, and 9 are workspace-local. Do not load them until a
workspace is entered — run `/prime` to load global context and select a
workspace, or `/switch` to change workspace mid-session.

## Repository layout

Each scope (global and every workspace) uses the same numbered sub-structure:

- `01-context/` — canvas context blocks (the who/what/why)
- `02-skills/` — requests and procedures (block 9 lives in `02-skills/9-requests/`)
- `03-data/` — data sources the scope reads from
- `04-automations/` — automated tools and scripts
- `05-deliverables/` — outputs produced

Top level:

- `01-global/` — global canvas blocks (1, 2, 3, 4, 8), shared by every workspace.
- `02-workspaces/01-commercial/`, `02-workspaces/02-race-operations/` — the two
  tracked workspaces. Each holds its own `CLAUDE.md`, `decision-log.md`, `todo.md`,
  and the numbered sub-structure above.
- `03-personal/` — local-only, gitignored personal workspace.
- `AI-Strategy-Canvas.pdf` — the reference framework this repo instantiates.

## Canvas block map

| Block | Name | Scope | Location |
|-------|------|-------|----------|
| 1 | Target Audience | Global | `01-global/01-context/1-target-audience.md` |
| 2 | Company | Global | `01-global/01-context/2-company.md` |
| 3 | Products/Services | Global | `01-global/01-context/3-products-services.md` |
| 4 | Context | Global | `01-global/01-context/4-context.md` |
| 5 | Role | Workspace | `02-workspaces/<workspace>/01-context/5-role.md` |
| 6 | Style/Brand Voice | Workspace | `02-workspaces/<workspace>/01-context/6-voice.md` |
| 7 | Resources | Workspace | `02-workspaces/<workspace>/01-context/7-resources.md` |
| 8 | Rules | Global, extendable | `01-global/01-context/8-rules.md` + workspace extensions |
| 9 | Request | Workspace | `02-workspaces/<workspace>/02-skills/9-requests/` |

## Cascade rules

1. **Inherit**: A workspace inherits every global block it does not mention.
2. **Extend**: A workspace may add to a global block. Rules (block 8) may ONLY be
   extended, never overridden. Global rules always apply.
3. **Override**: A workspace may replace blocks 5, 6, or 7 entirely. Overrides must
   be declared in the workspace CLAUDE.md so divergence from global strategy is
   visible and deliberate.

## Registered workspaces

- `02-workspaces/02-race-operations/` | Trackside and factory decision support
- `02-workspaces/01-commercial/` | Sponsorship, partnerships, and fan-facing commercial work
- `03-personal/` | Local-only, gitignored, general/personal tasks — behaves like
  Top-level (global blocks only, no 5/6/7/9 files) but with a private action
  list. Never synced to the shared repo. Auto-created on first selection if
  `03-personal/CLAUDE.md` or `03-personal/actions.md` doesn't exist yet.

## Entering a workspace

On entering a workspace (via `/prime` or `/switch`), load its `CLAUDE.md`
first. That manifest declares its inherit/extend/override posture, then
load the local block files it lists.

Personal is the exception: it's gitignored rather than tracked, and its
`CLAUDE.md` declares no local blocks at all (no 5/6/7/9). If
`03-personal/CLAUDE.md` or `03-personal/actions.md` is missing when Personal is
selected, create both before proceeding — see `03-personal/CLAUDE.md`'s own
"Auto-provisioning" section for the exact contents. No `.gitignore` change
is needed; `03-personal/` is already excluded.

## Action lists

- `03-personal/actions.md` — local-only, gitignored, spans all workspaces.
- `02-workspaces/<workspace>/todo.md` — shared, tracked in the repo, one per workspace.

Managed via `/actions` (see below for how new candidates get surfaced
during a session).

## Decision logs

- `02-workspaces/<workspace>/decision-log.md` — shared, tracked in the repo, one
  per workspace. Human-readable record of decisions made, each with a
  named owner and rationale, per the "own the call" value in
  `01-global/01-context/2-company.md`. For Race Operations this is the companion to the
  structured `03-data/decision-ledger.json`; populate both when running the
  `meeting-decision-analysis.md` request.

## Active action tracker

At the end of every turn, check whether the turn produced any:

- Explicit commitments ("I'll follow up on X", "I will draft Y next")
- Deferred items (something raised but deliberately postponed)
- Follow-ups that surfaced but won't be completed in the current session

If none of these appeared, do nothing — most turns generate no candidates,
and no note should be added when that's the case.

When candidates do appear:

1. **Check first.** Before surfacing anything, read `03-personal/actions.md`
   and, if a workspace is loaded, that workspace's `todo.md`.
2. **Don't propose duplicates.** Drop any candidate that already appears on
   one of those lists, matching by substance, not just exact wording. Only
   genuinely new items proceed to the next step.
3. **Surface once, at the end of the turn**, as a single block, separate
   from the rest of the response:

   ---
   **Possible follow-ups from this turn** *(not logged — say which to add via `/actions`)*
   - [ ] `<description>` — suggested target: `personal` / `race-operations` / `commercial`
   ---

4. **Never add these automatically.** They are candidates for the user to
   confirm, typically via `/actions [target] add <description>`.
5. If every candidate turns out to already be tracked, skip the block
   entirely rather than saying so — silence is the signal that nothing new
   surfaced.

## Rules for every session

- Apply Block 8 global rules (`01-global/01-context/8-rules.md`) plus any active
  workspace's extensions at all times.
- Apply the active workspace's Block 6 voice to all outputs once a
  workspace is loaded.
- Recommendations are inputs to a named human's decision, never the
  decision itself.
