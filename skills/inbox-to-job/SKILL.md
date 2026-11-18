---
name: inbox-to-job
description: Triage one or more C2C inboxes so every email lands as an action, a job-activity note, or archive - matching each message to its job or claim, pulling out attachments (permits, invoices, estimates, photos, carrier letters), flagging conditions like permit approvals or adjuster deadlines, and drafting replies for approval. Use for "go through my inbox", "triage Phil's inbox", "sort the four inboxes", "what came in from carriers", or "log these emails to the jobs".
---

# Inbox to job

Read the `c2c-context` skill first.

**Why this exists:** information at C2C arrives by email to several inboxes (one person
manages four), and the job record in the CRM only knows what someone types into it. This
skill closes that gap. Each inbox needs a named owner before it is triaged (Phil, Jodi,
Stephanie, Blake per `c2c-context`).

## Steps

1. **Confirm scope:** which inbox(es), what time window, whose they are. With more than one
   inbox, keep them labeled separately in the output.
2. **Classify each thread** into one bucket:
   - `ACTION` - someone at C2C must do something (reply, sign, pay, schedule, approve).
   - `JOB LOG` - information that belongs on a job record (permit status, adjuster note,
     carrier letter, sub invoice, photos, estimate, inspection result).
   - `FYI` - worth knowing, no action.
   - `ARCHIVE` - marketing, notifications, spam.
3. **Match to a job.** Use claim number, property address, customer name, PO, or job
   number in the subject, body or attachments. If two jobs could match, say both and ask.
   If none match, mark `NO MATCH` and say what identifier is missing.
4. **Flag conditions** at the top regardless of bucket:
   - permit approved / rejected / needs info -> Jodi
   - adjuster or carrier deadline, reinspection, payment issued -> Phil
   - sub invoice -> run the `sub-invoice-intake` skill on it
   - signed contract -> Phil
   - customer complaint or review mention -> Stephanie
5. **Draft job-activity notes** for every `JOB LOG` item: one line, date, source, what
   changed, attachment names. These are ready to paste or post to the CRM.
6. **Draft replies** for `ACTION` items that need one. Short, factual, in the owner's voice
   (use the `voice-match` profile if they have one). Never promise a date or amount the
   email thread does not already support.

## Output

```
<INBOX> - <window> - <n> threads
FLAGS
- [Permit] 123 Main St - approved - Jodi
ACTION (<n>)
- <from> / <job> - <what> - draft below
JOB LOG (<n>) - notes ready for the CRM
- <job>: <date> <source>: <what changed> [<attachments>]
NO MATCH (<n>)
- <from> - <subject> - missing: <identifier>
FYI <n> / ARCHIVE <n>
```

## Rules

- Never send, archive, delete or move mail unless the owner says so for that batch.
- Never open links or run attachments from unknown senders; describe them instead.
- Never post to the CRM without approval until Andy has wired and tested the write path.
