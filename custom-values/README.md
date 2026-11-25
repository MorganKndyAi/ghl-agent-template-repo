# Custom values: 7 shared + 9 agent blocks

Create all 16 EMPTY by API first, then fill them one at a time (draft here, you approve, PUT by API, wait 5 s,
read back byte identical). The agent stays mode Off until every token its prompt names exists and is filled.

Files here: one per value. Rename each block file to its token (`agent_first_reply.md` -> `<prefix>_agent_first_reply.md`).
Each file holds exactly what goes in GHL; delete the `<!-- -->` comment before pushing.

## Shared values (account root, no folder)
Read by every agent in the account. If one already exists, reuse it; never overwrite a value another live agent reads
without your yes.
| GHL name | Token | Holds |
|---|---|---|
| Agent Name | `agent_name` | The persona's first name |
| Agent Position | `agent_position` | e.g. warranty specialist |
| Dealership Name | `dealership_name` | As the client says it in texts |
| Dealership City | `dealership_city` | City |
| Business Hours | `business_hours` | Plain words, e.g. 9am to 6pm Monday to Saturday |
| Agent Service Region | `service_region` | e.g. Canada |
| Formatting Rules - Agents | `agent_formatting_rules` | `agent_formatting_rules.md` |

## Agent blocks (folder `<Prefix> Agent Custom Values`, made in the UI)
Name each `<Prefix> Agent <Block>`. GHL makes the token from the name AT CREATION; a later rename keeps the old token.
| Block | Token | Owns |
|---|---|---|
| First Reply | `<prefix>_agent_first_reply` | The very first reply to the opener only: the intro test and the intro |
| Convo Flow | `<prefix>_agent_convo_flow` | The numbered questions, each with its exact line and its skip rule |
| Exact Lines | `<prefix>_agent_exact_lines` | Opt out, threatens to report, human handoff: word for word, then stop |
| Interrupts | `<prefix>_agent_interrupts` | Anything at any turn: busy, wrong number, who is this, bot, photos, reactions, team replied |
| Objections | `<prefix>_agent_objections` | Every rebuttal, one per situation, then carry on with the step |
| Call Requests | `<prefix>_agent_call_requests` | Asks for a call or a person |
| Not Interested Ladder | `<prefix>_agent_not_interested_ladder` | Declines: one exit, or numbered stages in order |
| Eligibility | `<prefix>_agent_eligibility` | The only stated facts that change what the agent says. Checked every reply |
| Recap | `<prefix>_agent_recap` | Reading the details back, corrections, and the yes that unlocks the CLOSE |

Finance agents add a `Cash Buyer` block and keep trade inside the Convo Flow.
Drop Eligibility or Recap only if the job has no stops or nothing to confirm, and delete their lines from the prompt.

## Rules for every block
- One owner per scenario. If two blocks could answer the same message, decide which one and say so inside both.
- Every branch ends in the words to send and where it lands next.
- Never paste another block's token. Name labels the prompt defines (FLOW, RECAP, CONFIRM...) in plain words.
- Exact lines come from the client's real texts, their playbook, or your own wording. Never invented.
- No size cap that matters (13,704 chars verified live). Split a block only when it does two jobs.
