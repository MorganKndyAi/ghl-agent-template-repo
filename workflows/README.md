# Workflows

The agent only replies. Everything it must DO (move a stage, tag, alert the team, stop) is a workflow.
You build each one in the GHL UI from its spec here. Claude cannot read workflow steps by API, so it checks your build
from screenshots and records what is live in the spec.

| Spec | Starts when | Lesson |
|---|---|---|
| `lead-source.md` | A new lead arrives | 4.1 Connect Your Lead Sources |
| `move-to-engaged.md` | The lead is engaged | 4.2 Build "Move to Engaged" |
| `move-to-do-not-contact.md` | The lead opts out | 4.3 Build "Move to Do Not Contact" |
| `follow-up-sequence.md` | The lead goes quiet | 4.4 Build a Follow-up Sequence |

## Rules for every workflow
- **A reply binds to the LAST message sent in the thread.** Nothing may send between the message you want answered
  and the Wait that reads the reply.
- **A workflow SMS fills one level of tokens.** Write `{{custom_values.agent_name}}` straight into the SMS, never a
  block that holds it.
- **Agent actions quote the exact phrase.** A Trigger a Workflow condition quotes the fixed words of the line the
  agent sends (`agent/ACTIONS.md`). Reword the line, reword the condition in the same change.
- **Publish first, then create the action** that triggers it.
- After building, send Claude a screenshot of every step and the settings tab. The spec gets updated to match.

## Spec layout (every file)
Trigger · Filters · Steps in order · Settings · Exits · Ids · Checked live
