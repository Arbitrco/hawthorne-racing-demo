---
description: Manage the personal actions list or a workspace todo list
---

Manage one of three lists:

| Target | File | Scope |
|---|---|---|
| `personal` | `03-personal/actions.md` | Local-only, gitignored, spans all workspaces |
| `race-operations` | `02-workspaces/02-race-operations/todo.md` | Shared, tracked in repo, Race Operations only |
| `commercial` | `02-workspaces/01-commercial/todo.md` | Shared, tracked in repo, Commercial only |

## Choosing a target

The user may name the target explicitly as the first word after `/actions`
(`personal`, `race-operations`, or `commercial`). If they don't:

- If a workspace is currently loaded this session (via `/prime` or
  `/switch`), target that workspace's `todo.md`.
- Otherwise (no workspace loaded, or Top-level), target
  `03-personal/actions.md`.

State which target was resolved before acting, unless it's already obvious
from context (e.g. immediately after naming it explicitly).

## Usage

Parse the user's invocation as follows, where `[target]` is the optional
explicit target from above and everything else follows it:

| Form | Behaviour |
|---|---|
| `/actions [target]` (no further args) | Read the resolved file and display the table as-is. If the file doesn't exist, tell the user and offer to create it with the standard preamble and headers for that target. |
| `/actions [target] add <description>` | Add a new row to the resolved file. Use the next unused `#` (numbering is independent per file — do not share a counter across targets). Mark `Captured` as `direct`. Ask for `Priority` if not obvious. For `personal`, also ask for `Area` (typically `Race Operations`, `Commercial`, or `Top-level`) if not obvious. For a workspace target, also ask for `Owner` (a named person — per the "own the call" value, no unowned rows) if not obvious. |
| `/actions [target] done <#>` | Set `Status` to `done` for that row in the resolved file. Do not delete it. |
| `/actions [target] <#>` | Show the full row for that number in the resolved file — every column, expanded vertically for readability. |
| `/actions [target] sweep` | Walk through every row with status `open` or `in-progress` in the resolved file. For each, ask: keep open / mark in-progress / mark blocked / mark done / edit. Apply changes after the user responds. |
| `/actions [target] edit <#>` | Ask which column to change, then update, in the resolved file. |
| Anything else | Treat as `/actions [target] add <description>` if it reads as an action; otherwise ask for clarification. |

## Rules

- Today's date is available in session context — use it for any timestamps.
- Never renumber existing rows. New rows get `max(#) + 1` within their own file.
- Preserve the preamble and column headers at the top of each file.
- After any write, briefly confirm what changed, including which target it went to (e.g. "Added #3 to Race Operations todo: Confirm tyre allocation for round 13 — Head of Strategy, High, open").
- If the user gives only a fragment ("add a thing about Sandy"), ask for the full action description before writing.
- `03-personal/` is gitignored — changes to `03-personal/actions.md` are local-only, never commit it.
- `todo.md` files under `02-workspaces/` are shared and tracked in the repo. Editing one changes a file other people will see; don't commit changes unless the user asks you to.
- A workspace's `todo.md` inherits that workspace's confidentiality rules (Block 8 extensions, e.g. R-OPS-1–3 or R-COM-1–3) — don't write Tier 1/Tier 2 confidential detail into a description that doesn't need it.
- This command works independent of whether canvas blocks are loaded, but resolving the default target depends on session state from `/prime`/`/switch` as described above.

## Display format for `/actions [target]` (no further args)

Render the table directly. If there are many `done` rows, default to hiding them and add a one-line note: `(N done items hidden — use /actions [target] sweep or read the file to see all)`.
