# Lead source: [WORKFLOW NAME]

Starts the conversation with every new lead and hands the thread to the agent.

## Trigger
- [the exact trigger, e.g. form submitted / opportunity created] · Filter: [pipeline, form, tag]

## Steps (in this order)
```
[Trigger]
  Assign to AI agent        [agent name] · status Inactive until go live
  [team alert, sheet row... anything else that sends or logs]
  SMS: opener               "[exact opener]"            <- the LAST message before the Wait
  Wait                      until the contact replies · timeout [minutes]
    on both outputs         Condition: contact replied?
      True                  nothing (the agent answers)
      False                 SMS: intro "[exact intro, with {{custom_values.agent_name}} written in]"
  Add to workflow           [follow-up sequence] on every output that should get follow-ups
```
- Assign comes first, so a fast reply already has the agent on it.
- The opener is last before the Wait. Anything sent after it steals the reply.
- If the opener does not say who you are, the intro on timeout does, and the agent's First Reply knows not to repeat it.

## Settings
| Setting | Value |
|---|---|
| Allow re-entry | [on / off, and why] |
| Stop on response | [on / off] |
| Time window | [hours, and the timezone] |

## Exits
[reply, opt out, removed by Move to Do Not Contact]

## Ids and checked live
- Workflow id: `[id]` · Published: YYYY-MM-DD
- Checked from screenshots: YYYY-MM-DD
