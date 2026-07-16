---
description: Switch Hawthorne Cortex workspace without reloading global canvas blocks
---

Switch the active Hawthorne Cortex workspace. The global canvas blocks
(`01-global/01-context/1-4.md`, `01-global/01-context/8-rules.md`) are already
loaded automatically from `CLAUDE.md` at session start and stay loaded — do
not re-read them.

Discard whatever workspace-local blocks (5, 6, 7) and request file (9) are
currently loaded before proceeding — they belong to the workspace being left.

## Step 1 — Ask the user which workspace to load

---

**Which workspace are you working in today?**

1. 🏁 Top-level — general business tasks, no functional area
2. 🛞 Race Operations — trackside and factory decision support: strategy
   meetings, debriefs, race weekend briefs
3. 🤝 Commercial — sponsorship, partnerships, and fan-facing commercial work
4. 👤 Personal — local-only tasks, never synced to the shared repo

---

Wait for the user's selection before proceeding.

## Step 2 — Load the workspace manifest and local blocks

For the selected workspace, load its `CLAUDE.md` first. That manifest
declares the workspace's inherit/extend/override posture against the global
blocks, then load the local block files it lists (all under the workspace's
`01-context/`):

| Selection | Workspace manifest | Local blocks (in `01-context/`) |
|---|---|---|
| 1 — Top-level | None | Global only, no workspace blocks |
| 2 — Race Operations | `02-workspaces/02-race-operations/CLAUDE.md` | `5-role.md`, `6-voice.md`, `7-resources.md` |
| 3 — Commercial | `02-workspaces/01-commercial/CLAUDE.md` | `5-role.md`, `6-voice.md`, `7-resources.md` |
| 4 — Personal | `03-personal/CLAUDE.md` | None — global only, plus a private action list |

Apply the cascade rules from the root `CLAUDE.md` (inherit / extend /
override) exactly as the workspace manifest declares them. Rules (block 8)
may only be extended by a workspace, never overridden — global rules from
`01-global/01-context/8-rules.md` always apply in full.

### Personal workspace auto-provisioning

If `03-personal/CLAUDE.md` or `03-personal/actions.md` doesn't exist yet when
Personal is selected, create both before continuing:
- `03-personal/CLAUDE.md` — declares inherit-everything posture, no 5/6/7/9
  local blocks. Use the copy already in this repo as the template; if it's
  somehow also missing, write a manifest matching the other workspaces'
  `CLAUDE.md` format but with every block marked Inherit/None.
- `03-personal/actions.md` — empty action list using the same table format as
  `02-workspaces/<workspace>/todo.md`

`03-personal/` is already covered by `.gitignore` — no gitignore edit is
needed. Don't ask the user for confirmation before creating these two
files; it's a private, reversible, local-only scaffold.

### Requests (block 9)

Do not preload `9-requests/`. Once a task is underway, check the
workspace's `02-skills/9-requests/` folder for a request file matching the
task and load only that file before proceeding:

| Workspace | Request file | Covers |
|---|---|---|
| Race Operations | `02-skills/9-requests/meeting-decision-analysis.md` | Decision extraction, bias detection, ledger updates from a meeting transcript |
| Commercial | `02-skills/9-requests/monthly-sponsor-report.md` | Monthly sponsor performance report generation |

If a task doesn't match a defined request, complete it using the loaded
global and workspace blocks, respecting all rules in force.

## Step 3 — Confirm and resume the session

Respond with a brief confirmation in this format:

---

**Switched to [Workspace].**

**Context loaded:**
- Global canvas blocks (unchanged)
- [Workspace] role, voice, and resources — or "Top-level, no workspace loaded"
  — or "Personal, global blocks only" (note if `03-personal/` was just created)

**Requests available:**
- [Workspace]: [list request file names, or "none yet" for Top-level and Personal]

**What would you like to work on?**

---

## Rules for this session

Unchanged from `/prime`: apply the new workspace's Block 6 voice, apply
Block 8 global rules plus the active workspace's extensions (R-OPS-1–3 or
R-COM-1–3), follow the matching request file's steps and output contract
when one exists, and keep Tier 1/Tier 2 confidential data inside its own
workspace.
