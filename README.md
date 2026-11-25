# Your Agent Repo

The repo you build your first GoHighLevel Conversation AI text agent in, with Claude Code. One repo = one agent in
one sub-account. GHL has no version history for your agent, so this repo is it: every word the agent sends, every
setting, every change and how to undo it.

The repo for the course **Your First GHL AI Agent**. Each folder matches a lesson.

## Set up (lesson 1.1)
1. Go to [claude.ai/code](https://claude.ai/code) and sign in with GitHub. Needs a Pro plan or higher.
2. On this repo's GitHub page, click **Use this template** to make your own copy. Make it **private**: it will hold
   real conversations.
3. Install the Claude GitHub App on your copy, so Claude Code can open a private repo.
4. In claude.ai/code, pick your copy and start a session.
5. Connect your GHL sub-account. Your Private Integration token goes in the environment as a **network secret**
   (allowed website `services.leadconnectorhq.com`). Your location ID goes in as an environment variable,
   `GHL_LOCATION_ID`.
6. Tell Claude: **"Connect to my GHL account."** It reads your account back and says its name.
7. Tell Claude: **"Start a new agent."** It reads `CLAUDE.md` and asks you questions before it builds anything.

Your token never goes in a file, and never goes to GitHub.

## What is in here, and why
Top to bottom, in the order you use it.

**`plan/`: what the agent needs to know** (lessons 1.3, 1.4)
The agent only knows what you give it. Anything missing, it makes up.
- `real-conversations/`: real threads of a person doing this job by hand. The voice, the questions and the order come from here.
- `CONTEXT-CHECKLIST.md`: every question to answer before building, and where each answer goes.
- `PLAYBOOK.md`: the whole conversation written down, start to finish.

**`agent/`: the agent itself** (lessons 2.1 to 2.4)
- `SYSTEM-PROMPT.md`: who the agent is, its goal, and when to use each custom value. Read on every reply, so it stays short.
- `ACTIONS.md`: what the agent saves (lead details) and which workflows it fires.
- `SETTINGS.md`: every setting as you built it, so it can be checked and rebuilt.

**`custom-values/`: everything the agent says** (lessons 3.1, 3.2)
The questions in order, the exact lines, objections, interrupts. Kept out of the prompt so the prompt stays short, and
each one lives in one place you can find and fix.

**`knowledge-base/`: straight answers** (lesson 3.3)
Direct question, direct answer. Hours, prices, coverage. One answer, the same way every time.

**`workflows/`: everything the agent does** (lessons 4.1 to 4.4)
The agent only replies. Sending the opener, moving stages, alerting the team and stopping are all workflows.

**`testing/`: proof it works** (lessons 5.1, 5.2)
Every test before go live, run 3 times, and what you watched for after.

**`VERSION.md`, `CHANGELOG.md`, `snapshots/`: the history** (every lesson)
GHL keeps no history of your agent. These do. `VERSION.md` is the version that is live now. `CHANGELOG.md` is every
change with how to undo it. `snapshots/` is what was live before each change.

**`CLAUDE.md`: the rules Claude follows**
Ask before building, show every change before making it, read it back after, never delete without your yes, log everything.

**`.env.example`: only if you run Claude Code on your own computer**
On claude.ai/code your keys live in the environment instead (step 5 above).

## The 4 parts of an agent
| Part | Holds | Why it lives there |
|---|---|---|
| **System prompt** | Identity, tone, the goal, and one line per block saying WHEN to use it | Read on every reply. Keep it lean. |
| **Custom values** | Anything with an order or exact wording: first reply, the questions, objections, exact lines | One place per scenario, editable and checkable word for word |
| **Knowledge base** | Direct question, direct answer | It looks up one answer at a time. It cannot count, remember or know where it is in a conversation. |
| **Workflows** | Everything that happens around the agent: assign it, send the opener, move stages, alert the team | The agent only replies. Anything it must DO is a workflow. |

The same content never lives in two places. If a block owns it, the knowledge base does not.

## Build order
1. Plan: fill `plan/CONTEXT-CHECKLIST.md` from real conversations, then the playbook.
2. Create the agent, mode Off.
3. Write the system prompt.
4. Capture lead details: contact fields, then one Contact Info action per field.
5. Configure the agent settings.
6. Custom values: shared values, then each block, one at a time.
7. Knowledge base.
8. Workflows: lead source first, then each stage, then the follow-up.
9. Test everything, then go live.
10. After go live, every change goes through the loop in `CLAUDE.md`.

