# Instructions for Claude: building a GHL Conversation AI text agent

This repo holds ONE agent for ONE GoHighLevel sub-account. It is the agent's source of truth and its history.
The live account is where it runs. The person you are working with is "the builder".

## The rules (never break these)
1. **Ask before you build.** When the builder says "start a new agent", work through `plan/CONTEXT-CHECKLIST.md`
   with them, one section at a time, one question at a time. Never invent a line, a price, a fact or a rule. A gap is
   written down as a gap.
2. **Read before you write.** Before any change to the live account, read what is there now and save it to
   `snapshots/` (dated file). No snapshot, no write.
3. **Show it, then ask.** Show the exact change (before and after text, or the exact request) and wait for the
   builder's yes for THAT change. A yes for one change is not a yes for the next.
4. **Read back after every write.** Wait 5 seconds, read it back, and confirm it matches the repo byte for byte.
5. **Never delete without a named yes.** Before deleting anything (custom value, field, action, workflow, KB entry,
   file), name it, its id, what it holds and what uses it. Wait for a yes on that exact item.
6. **Log every live change.** A line in `CHANGELOG.md` (what, when, the id, how to undo it) and a version in
   `VERSION.md`. Then commit, naming each file (never `git add -A`), and push.
7. **Never handle the token.** On claude.ai/code it is a network secret on the environment and you never see it.
   On a computer it is in `.env`. Never print it, never write it in any other file, never commit `.env`.
8. **Hold changes while a real lead is mid conversation** with the agent. Wait until the thread goes quiet.

## Connecting to GHL
- `GHL_LOCATION_ID` is an environment variable.
- The token: on claude.ai/code the environment's network secret adds the `Authorization` header to calls to
  `services.leadconnectorhq.com`. On a computer, read `GHL_TOKEN` from `.env` and send `Authorization: Bearer <token>`.
- Base URL `https://services.leadconnectorhq.com`. Headers on every call: `Accept: application/json`,
  `User-Agent: curl/8.7.1` (without it some calls get a Cloudflare `403 Error 1010`).
- `Version: 2021-07-28` on location, custom value, contact and knowledge base calls.
  `Version: v3` on every `/conversation-ai/...` call.
- First call of every session: `GET /locations/{GHL_LOCATION_ID}`. Say the location name back to the builder before
  doing anything else. The token decides which account you touch; nothing else warns you.
- Custom value responses can hold raw newlines inside values. Parse with `json.loads(raw, strict=False)`.

## Build order (each step is a lesson)
1. **Plan.** `plan/CONTEXT-CHECKLIST.md`, from `plan/real-conversations/`, then `plan/PLAYBOOK.md`.
2. **Create the agent**, mode Off. The builder creates it in the GHL UI (or you create it by API,
   `POST /conversation-ai/agents`, if they ask). Read it back by API and record its id in `agent/SETTINGS.md`.
3. **System prompt.** Fill `agent/SYSTEM-PROMPT.md`. Push it by API as `fullPrompt`, never pasted in the UI (a paste
   strips blank lines). Every later prompt change: `PUT /conversation-ai/agents/{id}` resending every current setting.
4. **Capture lead details.** Contact fields (TEXT), then one Contact Info action per field (`agent/ACTIONS.md`).
5. **Agent settings.** The builder sets them in the UI. Record what they chose in `agent/SETTINGS.md`.
6. **Custom values.** Read every existing value first and reuse shared ones. Create each new value empty, then fill
   one at a time (`custom-values/README.md`). Folders are made in the UI; the API cannot make them.
7. **Knowledge base.** `knowledge-base/knowledge-base.json`, direct question and direct answer only.
8. **Workflows.** Built by the builder in the GHL UI from the specs in `workflows/`. Workflow steps cannot be read by
   the API: check the build from the builder's screenshots. Each Trigger a Workflow action is created after its
   workflow is published.
9. **Test** with `testing/TEST-PLAN.md`. Go live only on the builder's yes.

## After go live: every change goes through this loop
1. Read the real thread by API: every message, its time, and the contact's activity (actions fired, fields filled).
2. Find the exact line or rule that caused it. Search the prompt and every block.
3. Look at what the real person does in `plan/real-conversations/` before inventing a fix.
4. Propose the smallest change as before and after text. One decision at a time.
5. Hold it while a real lead is mid conversation.
6. Snapshot, write, wait 5 seconds, read back.
7. `CHANGELOG.md`, `VERSION.md`, commit by name, push.
8. Watch the next real lead for that exact fix. Say what you are watching for.

## How the agent texts (applies to agent content, not to your chat with the builder)
No apostrophes. Plain text. The agent's own words are 160 characters or less with no exclamation marks. Lines written
for it go out exactly as written. Full rules: `custom-values/agent_formatting_rules.md`.

## When you are not sure
Say "I have not checked that" and check it. Never state how GHL works, a limit or a default you have not seen in this
account, in GHL's docs, or in a build that already works.
