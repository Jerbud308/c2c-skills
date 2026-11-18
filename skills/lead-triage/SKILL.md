---
name: lead-triage
description: Sort C2C's open leads (storm, inbound calls, web forms, missed calls) into a short call-today list, draft the first-touch text or email for each, and list the screener questions still unanswered. Use when Blake asks "what leads do I call today", "triage the pipeline", "who's hot", "go through the storm leads", or when leads are piling up faster than they can be called.
---

# Lead triage

Read the `c2c-context` skill first.

**Why this exists:** in November 2026 there were 24 leads sitting in the pipeline and Blake
could only work a fraction of them. The fix is not more calling, it is calling the right
five first and letting a first-touch message do the rest.

## Inputs

The open leads from the CRM (export, screenshot or list pasted in). For each lead, whatever
exists: name, address, source, date in, job type, notes, last contact.

## Steps

1. **Clean the list.** Merge duplicates (same phone, email or address). Drop leads already
   marked won, lost or booked. Say how many you dropped and why.
2. **Score each lead 1 to 5** on these, and show the reasons in a few words:
   - Urgency: active leak, storm damage, insurance deadline, tarp needed = high.
   - Fit: job type C2C does (roofing, restoration, insurance claim, commercial maintenance).
   - Value signal: commercial property, full replacement, multiple units, property manager.
   - Freshness: hours since they came in. A lead goes cold fast; under 24 hours scores up.
   - Contact quality: has a phone number and a real address.
3. **Build the call-today list:** the top 5, highest score first, each with one line on
   why and the best number. Everything else goes to "first-touch only".
4. **Draft a first-touch message** for every lead not on the call list. Text if there is a
   mobile number, otherwise email. Plain, short, local, no hype:
   - who we are, that we got their request, one question that moves it forward
     (for example "Is water coming in right now, or is this from the last storm?").
   - Include "Reply STOP to opt out" on texts.
5. **Screener gaps:** for each lead, the questions still unanswered before Blake should
   spend time on it: address, type of damage, insurance claim filed (yes/no, carrier),
   owner or tenant, decision-maker, timeline.

## Output

```
CALL TODAY (5)
1. <name>, <town> - <why, 6 words> - <phone>
...
FIRST-TOUCH DRAFTS (<n>) - approve to send
- <name>: "<message>"
STILL NEED TO ASK
- <name>: <missing items>
DROPPED (<n>): <reason counts>
```

## Rules

- Never send. Blake (or the screener) approves the drafts.
- Never make up damage, insurance status or urgency the lead did not state.
- If a lead mentions an active leak or safety issue, put it at the top regardless of score
  and say so.
