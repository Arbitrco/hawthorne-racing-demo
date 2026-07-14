# Hawthorne Racing | Project Instructions

This file is loaded automatically at the start of every Claude Code session
in this repo. It is the root manifest for the Hawthorne Racing AI Brain: it
maps the workspace to the nine blocks of the AI Strategy Canvas, defines
what loads globally versus what loads per workspace, and sets the standing
rules for the session.

## Load instruction (session start)

The following are loaded automatically as part of this file being read.
No manual step is required for these:

- `canvas/1-target-audience.md`
- `canvas/2-company.md`
- `canvas/3-products-services.md`
- `canvas/4-context.md`
- `canvas/8-rules.md`

Blocks 5, 6, 7, and 9 are workspace-local. Do not load them until a
workspace is entered — run `/prime` to load global context and select a
workspace, or `/switch` to change workspace mid-session.

## Canvas block map

| Block | Name | Scope | Location |
|-------|------|-------|----------|
| 1 | Target Audience | Global | `canvas/1-target-audience.md` |
| 2 | Company | Global | `canvas/2-company.md` |
| 3 | Products/Services | Global | `canvas/3-products-services.md` |
| 4 | Context | Global | `canvas/4-context.md` |
| 5 | Role | Workspace | `workspaces/<name>/5-role.md` |
| 6 | Style/Brand Voice | Workspace | `workspaces/<name>/6-voice.md` |
| 7 | Resources | Workspace | `workspaces/<name>/7-resources.md` |
| 8 | Rules | Global, extendable | `canvas/8-rules.md` + workspace extensions |
| 9 | Request | Workspace | `workspaces/<name>/9-requests/` |

## Cascade rules

1. **Inherit**: A workspace inherits every global block it does not mention.
2. **Extend**: A workspace may add to a global block. Rules (block 8) may ONLY be
   extended, never overridden. Global rules always apply.
3. **Override**: A workspace may replace blocks 5, 6, or 7 entirely. Overrides must
   be declared in the workspace CANVAS.md so divergence from global strategy is
   visible and deliberate.

## Registered workspaces

- `workspaces/race-operations/` | Trackside and factory decision support
- `workspaces/commercial/` | Sponsorship, partnerships, and fan-facing commercial work

## Entering a workspace

On entering a workspace (via `/prime` or `/switch`), load its `CANVAS.md`
first. That manifest declares its inherit/extend/override posture, then
load the local block files it lists.

## Action lists

- `personal/actions.md` — local-only, gitignored, spans all workspaces.
- `workspaces/<name>/todo.md` — shared, tracked in the repo, one per workspace.

Managed via `/actions` (see below for how new candidates get surfaced
during a session).

## Decision logs

- `workspaces/<name>/decision-log.md` — shared, tracked in the repo, one
  per workspace. Human-readable record of decisions made, each with a
  named owner and rationale, per the "own the call" value in
  `canvas/2-company.md`. For Race Operations this is the companion to the
  structured `data/decision-ledger.json`; populate both when running the
  `meeting-decision-analysis.md` request.

## Active action tracker

At the end of every turn, check whether the turn produced any:

- Explicit commitments ("I'll follow up on X", "I will draft Y next")
- Deferred items (something raised but deliberately postponed)
- Follow-ups that surfaced but won't be completed in the current session

If none of these appeared, do nothing — most turns generate no candidates,
and no note should be added when that's the case.

When candidates do appear:

1. **Check first.** Before surfacing anything, read `personal/actions.md`
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

- Apply Block 8 global rules (`canvas/8-rules.md`) plus any active
  workspace's extensions at all times.
- Apply the active workspace's Block 6 voice to all outputs once a
  workspace is loaded.
- Recommendations are inputs to a named human's decision, never the
  decision itself.
