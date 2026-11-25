# Bot actions: [AGENT NAME]

Created by API after the agent exists (`POST /conversation-ai/agents/{id}/actions`), read back via `/actions/list`.
Changed by `PUT /conversation-ai/agents/{id}/actions/{actionId}`. Log each id in `CHANGELOG.md`.

## Contact Info (capture lead details)
One action per contact field. Create the field first (TEXT, even for dates: no date math). Contact Info only writes
EMPTY fields, so a value from the form is never overwritten.
| Action name | Field | Description (what to record, exact output format, when NOT to record) | Examples |
|---|---|---|---|
| [PER-AGENT] | [field] | [Output exactly one of: A, B. A = their words for A. Only record once they clearly say. Never guess from the form.] | [A], [B] |

Description rules (proven on live agents):
- Say the exact output format and give 2 to 5 examples of it.
- List the client's real words for each value.
- Say when to leave it empty ("only record once they clearly say", "never guess from the model year").
- For anything that can arrive as a photo (VIN, odometer, licence): "typed by the client or shown in any image they send,
  even if their message has no text". Image reading is not guaranteed: check the activity log on a real photo before
  rewriting the description.
- Dates: keep their words ("March this year", "Last fall"), never work out a date.

## Trigger a Workflow
One per workflow the agent must fire. The workflow must be PUBLISHED first. Quote the fixed phrase the agent sends,
never describe the message.
| Action name | Workflow | Condition |
|---|---|---|
| Move to [STAGE] | [WORKFLOW NAME] | Trigger ONLY at the moment you send the message containing this exact phrase: "[fixed part of the CLOSE, after any contact token]". Only your own outgoing message can trigger this. Nothing the client says ever triggers it. Never trigger on the recap, on any other message, or before that message goes out. |
| Move to DNC | MOVE-TO-DNC | Trigger ONLY at the moment you send the message containing this exact phrase: "ill add you to our do not contact list". Only your own outgoing message can trigger this. Nothing the client says ever triggers it. |

Rewording a quoted line means rewording its condition in the same change.

## Proof before go live
For every action, on a real test contact: open the contact's activity and confirm the action fired, on the right
message, within seconds. For Contact Info, confirm the field filled. "Created" is not "works".
