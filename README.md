# GHL Agent Template Repo

The starting point for building a GoHighLevel Conversation AI text agent with Claude Code. One repo = one agent in
one sub-account. The folders start empty. You and Claude fill them as you build.

GHL keeps no history of your agent. This repo is the history: every word the agent sends, every setting, every change
and how to undo it.

## Set up
1. Go to [claude.ai/code](https://claude.ai/code) and sign in with GitHub. Needs a Claude Pro plan or higher.
2. On this page, click **Use this template** to make your own copy. Make it **private**: it will hold real conversations.
3. Install the Claude GitHub App on your copy, so Claude Code can open a private repo.
4. In claude.ai/code, pick your copy and start a session.
5. Connect your GHL sub-account. Your Private Integration token goes in the environment as a **network secret**
   (allowed website `services.leadconnectorhq.com`). Your location ID goes in as an environment variable, `GHL_LOCATION_ID`.
6. Tell Claude: **"Connect to my GHL account."** It reads your account back and says its name.
7. Tell Claude: **"Start a new agent."**

Your token never goes in a file, and never goes to GitHub.

## What goes where
| Folder | What goes in it |
|---|---|
| `plan/` | `real-conversations/`: real text threads of a person doing this job by hand, one file per thread, names and numbers replaced. `playbook.md`: the whole conversation written down, start to finish. |
| `agent/` | `system-prompt.md`: who the agent is, its goal, and when to use each custom value. `actions.md`: the lead details it saves and the workflows it fires. `settings.md`: every setting as built, plus the agent id. |
| `custom-values/` | One file per custom value, named by its token (`paid_lead_first_reply.md`). Holds exactly what goes in GHL. |
| `knowledge-base/` | `knowledge-base.json`: direct question, direct answer. |
| `workflows/` | One file per workflow: trigger, steps in order, settings, ids. |
| `backups/` | A copy of what was live in GHL right before each change (`YYYY-MM-DD-<what>.json`). How a change gets undone, even if someone edited it in GHL by hand. |
| `VERSION.md` | The version that is live now, and what each version changed. |
| `CHANGELOG.md` | Every change pushed to the live account, with how to undo it. |

## The 4 parts of an agent
| Part | Holds | Why |
|---|---|---|
| System prompt | Identity, tone, the goal, and one line per custom value saying when to use it | Read on every reply with the whole thread, so it stays short |
| Custom values | Everything with an order or exact wording | One place per scenario, easy to find and fix |
| Knowledge base | Direct question, direct answer | It looks up one answer at a time. It cannot remember where it is in a conversation. |
| Workflows | Everything the agent does: send the opener, move stages, alert the team, stop | The agent only replies |

The same content never lives in two places. If a custom value owns it, the knowledge base does not.

## Custom values
**Shared** (every agent in the account reads these; reuse them if they exist):
| Name in GHL | Token |
|---|---|
| Agent Name | `agent_name` |
| Agent Position | `agent_position` |
| Dealership Name | `dealership_name` |
| Dealership City | `dealership_city` |
| Business Hours | `business_hours` |
| Agent Service Region | `service_region` |
| Formatting Rules - Agents | `agent_formatting_rules` |

**Agent blocks** (named `<Agent> <Block>`, e.g. `Paid Lead First Reply` makes `paid_lead_first_reply`):
| Block | Holds |
|---|---|
| First Reply | The client's very first reply to the opener: check if an intro went out, then the intro |
| Interrupts | Checked before every reply: wrong number, who is this, are you a bot, busy, a team member replied |
| Convo Flow | The steps in order: each question, and when to skip it because it is already on file |
| Cash Buyer | The moment they say cash: their budget first, never ask for credit details |
| Objections | Every rebuttal, then back to the step |
| Not Interested Sequence | What to send each time they say no, in order |
| Call Requests | They ask for a call or a person |
| Exact Lines | Lines sent word for word: opt out, threatens to report, human handoff |

GHL makes the token from the name when the value is CREATED. Renaming it later keeps the old token. Folders are made
in the GHL UI; the API cannot make them.

## Build order
1. Plan: real conversations, then the playbook.
2. Create the agent, mode Off.
3. Write the system prompt.
4. Capture lead details: contact fields, then one Contact Info action per field.
5. Configure the agent settings.
6. Custom values: the shared ones, then each block, one at a time.
7. Knowledge base.
8. Workflows: lead source, Move to Engaged, Move to Do Not Contact, the follow-up sequence.
9. Test, then go live.
10. After go live, every change goes through the loop below.

---

# Rules for Claude

## Always
1. **Ask before you build.** Work through the plan with the builder one question at a time. Never invent a line, a
   price, a fact or a rule. A gap gets written down as a gap.
2. **Read before you write.** Before any change to the live account, read what is there and save it to `backups/`.
3. **Show it, then ask.** Show the exact change and wait for the builder's yes for THAT change.
4. **Read back after every write.** Wait 5 seconds, read it back, and confirm it matches the repo exactly.
5. **Never delete without a named yes.** Name it, its id, what it holds and what uses it. Wait for a yes on that item.
6. **Log every live change** in `CHANGELOG.md` and `VERSION.md`, then commit naming each file, and push.
7. **Never handle the token.** On claude.ai/code it is a network secret and you never see it. On a computer it is in
   `.env`, which never gets committed. Never print it or write it anywhere.
8. **Hold changes while a real lead is mid conversation.**
9. **Not sure? Say "I have not checked that" and check it.** Never state how GHL works unless you saw it in this
   account, in GHL's docs, or in a build that already works.

## Connecting to GHL
- Base URL `https://services.leadconnectorhq.com`. On claude.ai/code the network secret adds the `Authorization` header.
  On a computer, send `Authorization: Bearer <GHL_TOKEN from .env>`.
- Every call: `Accept: application/json` and `User-Agent: curl/8.7.1` (without it some calls get a Cloudflare `403 Error 1010`).
- `Version: 2021-07-28` on location, custom value, contact and knowledge base calls. `Version: v3` on `/conversation-ai/...` calls.
- First call of every session: `GET /locations/{GHL_LOCATION_ID}`. Say the account name back before anything else.
- Custom value responses can hold raw newlines inside values. Parse with `json.loads(raw, strict=False)`.

## Building
- The system prompt is pushed by API as `fullPrompt`, never pasted in the UI (a paste strips blank lines).
- Contact fields are TEXT, even dates. Contact Info only fills EMPTY fields.
- A Trigger a Workflow condition quotes the exact fixed words of the line the agent sends: `Trigger ONLY at the moment
  you send the message containing this exact phrase: "<words>". Only your own outgoing message can trigger this.` Reword
  the line, reword the condition in the same change.
- Workflows are built by the builder in the GHL UI. Their steps cannot be read by API, so check them from screenshots.
- A reply binds to the last message sent. Nothing may send between the opener and the Wait that reads the reply.

## Before go live
Run each test 3 times: the whole conversation, every interrupt, every objection, the not interested sequence in
order, a knowledge base question, a question it cannot answer, an opt out, and every action (check the contact's
activity). Never test on a phone number a workflow notification sends to.

## After go live: every change
1. Read the real thread by API: every message, its time, and the contact's activity.
2. Find the exact line or rule that caused it.
3. Check what the real person does in `plan/real-conversations/` before inventing a fix.
4. Propose the smallest change as before and after text. One decision at a time.
5. Hold it while a real lead is mid conversation.
6. Back up, write, wait 5 seconds, read back.
7. `CHANGELOG.md`, `VERSION.md`, commit, push.
8. Watch the next real lead for that exact fix.

## How the agent texts
No apostrophes. Plain text. Anything the agent writes itself is 160 characters or less with no exclamation marks.
Lines written for it go out exactly as written. These rules live in `agent_formatting_rules`.
