# Move to Do Not Contact: [WORKFLOW NAME]

When a lead opts out: stop every message, pull them from every workflow, close the opportunity, turn the agent off.
The agent can say "ill add you to our do not contact list", but only this workflow makes that true.

## Triggers (both, in one workflow)
1. Contact DND: the lead texted STOP, so GHL turned on DND itself.
2. The agent's `Move to DNC` Trigger a Workflow action, quoting the phrase in its opt out line:
   "ill add you to our do not contact list" (`agent/ACTIONS.md`). This covers "remove me" and anything that is not STOP.

Use ONE workflow for both. Two separate opt out workflows that each remove the contact from all workflows remove each
other mid-run.

## Steps
```
[Trigger]
  Enable DND                all channels
  Remove from all workflows
  Find opportunity          most recent, pipeline [pipeline]
    Found                   Update opportunity: stage [DNC stage] · status Lost
                            Add tag: dnc
                            Turn off AI agent
    Not found               nothing
```

## Settings
| Setting | Value |
|---|---|
| Allow move to previous stage | ON |
| Allow re-entry | [on / off] |

## Ids and checked live
- Workflow id: `[id]` · Published: YYYY-MM-DD · Bot action id: `[id]`
- Proven on a test contact (both triggers): YYYY-MM-DD
