---
description: Switch Hawthorne Cortex workspace without reloading global canvas blocks
---

Switch the active Hawthorne Cortex workspace. The global canvas blocks
(`canvas/1-4.md`, `canvas/8-rules.md`) are already loaded automatically from
`CLAUDE.md` at session start and stay loaded — do not re-read them.

Discard whatever workspace-local blocks (5, 6, 7) and request file (9) are
currently loaded before proceeding — they belong to the workspace being left.

## Step 1 — Ask the user which workspace to load

---

**Which workspace are you working in today?**

1. 🏁 Top-level — general business tasks, no functional area
2. 🛞 Race Operations — trackside and factory decision support: strategy
   meetings, debriefs, race weekend briefs
3. 🤝 Commercial — sponsorship, partnerships, and fan-facing commercial work

---

Wait for the user's selection before proceeding.

## Step 2 — Load the workspace manifest and local blocks

For the selected workspace, load `workspaces/<name>/CANVAS.md` first. That
manifest declares the workspace's inherit/extend/override posture against
the global blocks, then load the local block files it lists:

| Selection | Workspace manifest | Local blocks |
|---|---|---|
| 1 — Top-level | None | Global only, no workspace blocks |
| 2 — Race Operations | `workspaces/race-operations/CANVAS.md` | `5-role.md`, `6-voice.md`, `7-resources.md` |
| 3 — Commercial | `workspaces/commercial/CANVAS.md` | `5-role.md`, `6-voice.md`, `7-resources.md` |

Apply the cascade rules from the root `CLAUDE.md` (inherit / extend /
override) exactly as the workspace manifest declares them. Rules (block 8)
may only be extended by a workspace, never overridden — global rules from
`canvas/8-rules.md` always apply in full.

### Requests (block 9)

Do not preload `9-requests/`. Once a task is underway, check the
workspace's `9-requests/` folder for a request file matching the task and
load only that file before proceeding:

| Workspace | Request file | Covers |
|---|---|---|
| Race Operations | `9-requests/meeting-decision-analysis.md` | Decision extraction, bias detection, ledger updates from a meeting transcript |
| Commercial | `9-requests/monthly-sponsor-report.md` | Monthly sponsor performance report generation |

If a task doesn't match a defined request, complete it using the loaded
global and workspace blocks, respecting all rules in force.

## Step 3 — Confirm and resume the session

Respond with a brief confirmation in this format:

---

**Switched to [Workspace].**

**Context loaded:**
- Global canvas blocks (unchanged)
- [Workspace] role, voice, and resources — or "Top-level, no workspace loaded"

**Requests available:**
- [Workspace]: [list request file names, or "none yet" for Top-level]

**What would you like to work on?**

---

## Rules for this session

Unchanged from `/prime`: apply the new workspace's Block 6 voice, apply
Block 8 global rules plus the active workspace's extensions (R-OPS-1–3 or
R-COM-1–3), follow the matching request file's steps and output contract
when one exists, and keep Tier 1/Tier 2 confidential data inside its own
workspace.
