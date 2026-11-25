# Move to Engaged: [WORKFLOW NAME]

Moves the lead's opportunity to Engaged once they are engaged.

## Trigger
[DECIDE: what counts as engaged for this agent, and what starts the workflow]
- Option A: the agent's Trigger a Workflow action, on the exact phrase of a line it sends at that point
  (`agent/ACTIONS.md`).
- Option B: Customer replied, filtered to contacts that do not have the `engaged` tag, with a step that decides if the
  reply shows real interest. GHL's built-in positive intent filter reads tone, not interest: "Im good" and "not
  interested" can both read as positive.

## Steps
```
[Trigger]
  Update opportunity        pipeline [pipeline] · stage Engaged
  Add tag                   engaged
```

## Settings
| Setting | Value |
|---|---|
| Allow move to previous stage | ON (with it OFF, a stage change on an opportunity that already moved can silently do nothing) |
| Allow re-entry | [on / off] |

## Ids and checked live
- Workflow id: `[id]` · Published: YYYY-MM-DD · Bot action id: `[id]`
- Checked from screenshots: YYYY-MM-DD · Proven on a test contact: YYYY-MM-DD
