---
name: meeting-to-tasks
description: Turn a C2C meeting transcript or notes (Granola, Zoom, Teams, a voice memo, typed notes) into verified action items with one owner and a date each, separating real decisions from ideas that were only floated, and drafting the follow-up message. Use for "what came out of that meeting", "action items from the call", "turn this into tasks", "who's doing what after the owners meeting", or "write the follow-up".
---

# Meeting to tasks

Read the `c2c-context` skill first.

## Steps

1. **Extract candidates:** every commitment ("I'll", "we need to", "can you", "by Friday"),
   every decision, every open question.
2. **Verify each against the transcript.** For each item, quote the line it came from (a
   few words) and classify:
   - `DECIDED` - someone with authority agreed.
   - `ACTION` - a named person agreed to do a specific thing.
   - `IDEA` - floated, not agreed. Do not turn it into a task.
   - `OPEN` - a question nobody answered.
   Summaries often promote ideas into decisions; this step stops that.
3. **Owner and date.** Each ACTION gets exactly one owner from `c2c-context` and the date
   they said. No date said = "no date", not an invented one.
4. **Dedupe** against the existing task list or CRM tasks if available.
5. **Draft the follow-up** message to attendees: decisions, actions with owners and dates,
   open questions. Short.

## Output

```
<meeting> - <date>
DECIDED
- <decision> ("<source words>")
ACTIONS
- [ ] <owner>: <task> - <date or no date>
OPEN QUESTIONS
- <question> - who should answer
IDEAS (not tasks)
- <idea>
FOLLOW-UP DRAFT
<message>
```

## Rules

- Never send the follow-up or create tasks in a system without approval.
- When the speaker is unclear in the transcript, say "unclear who said this" instead of
  guessing the owner.
