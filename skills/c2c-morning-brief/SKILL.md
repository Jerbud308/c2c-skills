---
name: c2c-morning-brief
description: A five-minute morning brief for a C2C owner or lead (Blake, Phil, Dave, Jodi, Marcus), tailored to their lane - what needs them today, what money is moving, what is stuck, and what can wait. Use when Blake, Phil, Dave, Jodi or Marcus says "morning brief", "what's on today", "what do I need to know", "catch me up", or at the start of the day from a scheduled run.
---

# C2C morning brief

Read the `c2c-context` skill first. Find who is asking and use their lane.

## Gather (only what is connected; say what was not available)

- Today's and tomorrow's calendar.
- Their inbox(es) since yesterday's brief: unread, flagged, and anything from a carrier,
  adjuster, property manager, sub, or customer with a job open.
- CRM: new leads, jobs that changed status, site visits today, signed contracts.
- Money (Phil and Dave): invoices waiting on approval, payments received, overdue AR.

## Shape by person

- **Blake:** new leads since yesterday (count + top 3 by urgency), site visits today,
  compliance items Jodi routed to him, anything a customer is waiting on him for.
- **Phil:** signed contracts, approvals waiting on him, AR that moved or went overdue,
  carrier and adjuster emails needing a reply, today's schedule conflicts.
- **Dave:** sub invoices in the queue (count and total), jobs missing receipts or bills,
  crews and jobs today, anything blocking a job from starting or closing.
- **Jodi:** permits approved, rejected or waiting on info; licenses, insurance certificates
  and training due in the next 30 days; compliance items she needs to route to Blake.
- **Marcus:** payroll week status (days logged vs. expected per worker), workers with no
  job assigned, payment problems carried from last week (bad bank account, paid through a
  crew lead).

## Output (fits on a phone screen)

```
<Name>, <weekday date>
NEEDS YOU TODAY
1. <item> - <why it is on you> - <link or where to find it>
2. ...
MONEY
- <in / out / waiting, with amounts from the source>
STUCK
- <item> - <who owns it>
CAN WAIT
- <count> items, ask for the list
```

## Rules

- Five "needs you" items maximum. If there are more, rank by money and deadline and say
  "<n> more, ask for them".
- Every amount comes from a system or document. No estimates.
- If a source was not reachable (inbox not connected, CRM down), say so in one line at the
  top. A quiet brief because a feed was broken is worse than no brief.
