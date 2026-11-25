# Follow-up sequence: [WORKFLOW NAME]

Texts a lead who went quiet, until they reply. The agent never texts first, so this workflow is the only follow-up.

## Who it is for
[DECIDE]
- Never replied to the opener: pre-written messages, written in the playbook.
- Replied, then went quiet mid conversation: each message picks up at the step they stopped on.
  A workflow AI step cannot see the text thread. Without the conversation given to it (for example a summary field the
  agent fills), it makes details up.

## Trigger
- Added by: [lead source workflow outputs / another workflow]

## Steps
| # | Wait | Message (exact) |
|---|---|---|
| 1 | [time] | "[message]" |

## Exits
- They reply: the workflow stops and the agent answers.
- Opt out: removed by Move to Do Not Contact.
- [anything else]

## Ids and checked live
- Workflow id: `[id]` · Published: YYYY-MM-DD
- Checked from screenshots: YYYY-MM-DD · Proven on a test contact: YYYY-MM-DD
