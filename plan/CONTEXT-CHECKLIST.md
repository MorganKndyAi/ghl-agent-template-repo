# Context Checklist: what an agent needs before anything gets built

The agent only knows what you give it. Every gap gets filled with something it makes up, and every line you write
goes out word for word to every lead. So the context comes first, from real conversations, and the client signs off
on it before it goes live.

Claude asks you each section, one at a time. Short answers are fine. The right column says where each answer lands.
Anything not answered stays a gap: write it down as a gap, never guess it.

## Sources (collect these first)
- [ ] **Real conversations.** 5 to 20 real threads of a person doing this job by hand, good and bad. These set the
      voice, the question wording and the order. Save them to `plan/real-conversations/`.
- [ ] **The client's playbook**, if one exists. A playbook is a starting point; their real texts beat it.
- [ ] **The form or lead source.** Every field a lead arrives with, and how often each is blank or "Not sure".
- [ ] **A call with the client** to answer the open questions below. Save the transcript verbatim.

## 1. The job
| Question | Lands in |
|---|---|
| What does this agent do, in one sentence? Who is it texting and what outcome does it drive? | Prompt: Personality |
| Definition of done: what has to be true for the agent to stop and hand over? (a recap confirmed, an appointment, a credit app) | Prompt: Goal |
| Who takes over after the agent is done, and how do they find out? | Close + stage workflow |
| Lead state: warm (just applied), cold (old data), existing client? | Prompt: Personality (tone) |
| Persona: agent name, position, dealership name, city, service region, business hours | Shared custom values |

## 2. How the conversation starts
| Question | Lands in |
|---|---|
| What starts it? (form submit, opportunity created, a list) | Lead source workflow trigger |
| The exact opener the workflow sends, and what happens if they do not reply | Lead source workflow + First Reply |
| Does the opener say who we are? If not, the agent introduces on the first reply | First Reply |
| What does the form already tell us? List every field token the agent can confirm or skip on | Prompt: WHAT THE FORM SENT |

## 3. What the agent collects
For EACH piece of information, answer all five:
| Info | Why we need it | Exact question to ask | Skip when | Where it goes in GHL |
|---|---|---|---|---|
| [e.g. new or used] | [what the team does with it] | [their wording, from real threads] | [form already has it] | [contact field, TEXT] |

Then: the ORDER they are asked in, which ones are optional (ask once, never block), and what to send when the client
does not have it or will not give it. Lands in: Convo Flow + `agent/ACTIONS.md` (one Contact Info action per field).

## 4. The words
| Question | Lands in |
|---|---|
| The close: the exact line sent when the job is done | Prompt: CLOSE + its Trigger a Workflow condition |
| The recap (if the team needs details confirmed): what is read back, in what order | Recap |
| Lines that must go out word for word: opt out, threatens to report, human handoff | Exact Lines |
| Busy, driving, at work, wrong number, who is this, are you a bot, sold it, sent a photo | Interrupts |
| The objections real leads raise, each with the line the client wants sent | Objections |
| Not interested: one polite exit, or a ladder of tries? The exact line for each stage | Not Interested Ladder |
| Call requests: the number, and what happens when they name a time | Call Requests |
| How the person texts: reactions they use, emoji or not, how long their texts are | Formatting Rules (REACTIONS) |

## 5. The facts
| Question | Lands in |
|---|---|
| Direct questions leads ask, each with one approved answer (hours, packages, prices, terms, coverage) | Knowledge base |
| Prices the agent may say, and the wording around them (before tax, exact quote confirms) | Knowledge base + Prompt: PRICES |
| What the agent must never say or promise | Prompt: HARD RULES |

## 6. The stops
| Question | Lands in |
|---|---|
| Who does the client NOT serve? Only stated facts, never the agent's judgement. Check each rule against real leads: how many would it block? | Eligibility |
| When does a human take over? (claims, complaints, anything not covered, no clear answer after two asks) | Exact Lines: HUMAN HANDOFF + a team alert workflow |
| What ends the conversation for good? (opt out, sold it, wrong number) | Exact Lines / Interrupts + Move to DNC workflow |

## 7. Sign off
- [ ] Every rule that turns a lead away checked with the client against real leads.
- [ ] Every exact line comes from the client's real texts, their playbook, or your own wording. None invented.
- [ ] Every gap listed, with who answers it.
