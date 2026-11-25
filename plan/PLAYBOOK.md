# Playbook: [AGENT NAME]

The conversation written down, start to finish, from `plan/real-conversations/` and the client's answers in
`plan/CONTEXT-CHECKLIST.md`. Every custom value block is built from this page. Write it in plain words; Claude turns
it into blocks.

## The job
- Who the agent texts: [who, and what they just did]
- The outcome: [what has to be true when it stops]
- Who takes over, and how they find out: [person or team + the workflow that alerts them]

## The opener
- The workflow sends: "[exact opener]"
- If they do not reply: [what goes out, and when]
- First reply from the agent: [does it introduce itself? the exact intro]

## The steps, in order
| # | Info | Exact question (their wording) | Skip when | Optional? | If they do not have it |
|---|---|---|---|---|---|
| 1 | [info] | "[question]" | [form already has it] | [yes / no] | "[what to send]" |

## The close
- Recap (if the team needs details confirmed): [what is read back, in what order]
- The close line: "[exact line]"
- What it triggers: [workflow + stage]

## Exact lines (go out word for word, then stop)
- Opt out: "[line]"
- Threatens to report: "[line]"
- Human handoff: "[line]"

## Interrupts (can happen at any turn)
| They say | The agent sends | Then |
|---|---|---|
| [busy / driving / wrong number / who is this / are you a bot / sent a photo] | "[line]" | [back to the step, or stop] |

## Objections
| Objection (their real words) | The line the client wants sent | Then |
|---|---|---|
| [objection] | "[line]" | [back to the step] |

## Not interested
- [one polite exit] OR [a ladder: 1st decline "[line]", 2nd "[line]", last "[line]"]

## Stops
- Who the client does not serve (stated facts only, checked against real leads): [rule] blocks [x of y] real leads
- When a human takes over: [cases]

## Open gaps
| Gap | Who answers it |
|---|---|
| [question] | [client / builder] |
