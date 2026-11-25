# Test plan: [AGENT NAME]

Run every case 3 times. The agent does not answer the same way twice, so one pass proves nothing.
Test on a real test contact, and never on a phone number that a workflow notification sends to (the notification
lands in the thread and the reply binds to it).

## Before go live
| # | Case | What must happen | Run 1 | Run 2 | Run 3 |
|---|---|---|---|---|---|
| 1 | The whole conversation, start to close | Every step asked once, nothing read back, the recap, the close | | | |
| 2 | Same message as the first reply and mid conversation | Routes differently | | | |
| 3 | Each interrupt (one row each) | Its line, then back to the step | | | |
| 4 | Each objection (one row each) | Its line, then back to the step | | | |
| 5 | Not interested, every stage in order | Each stage once, never skipped | | | |
| 6 | A direct question | The knowledge base answer | | | |
| 7 | A question it cannot answer | The human handoff line, and the team gets alerted | | | |
| 8 | Opt out | The exact line, then nothing. Moved to Do Not Contact | | | |
| 9 | Each Contact Info action | The field fills (check the contact) | | | |
| 10 | Each Trigger a Workflow action | Fired on the right message, within seconds (check the contact's activity) | | | |

"Created" is not "works". Every action is proven on the contact's activity before go live.

## After go live
For each change, note the real lead it was watched on and what happened.
| Date | Version | Watched for | Lead | Result |
|---|---|---|---|---|
| | | | | |
