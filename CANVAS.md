# Hawthorne Racing | Root Canvas Manifest

This is the master manifest for the Hawthorne Racing AI Brain. It maps the workspace
to the nine blocks of the AI Strategy Canvas and defines what loads globally versus
what loads per workspace.

## Load instruction (session start)

Load the following into context at the start of every session:

- `canvas/1-target-audience.md`
- `canvas/2-company.md`
- `canvas/3-products-services.md`
- `canvas/4-context.md`
- `canvas/8-rules.md`

Blocks 5, 6, 7, and 9 are workspace-local. Do not load them until a workspace is entered.

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

On entering a workspace, load its `CANVAS.md` first. That manifest declares its
inherit/extend/override posture, then load the local block files it lists.
