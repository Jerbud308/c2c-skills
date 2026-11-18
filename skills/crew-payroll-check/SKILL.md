---
name: crew-payroll-check
description: Check the weekly crew payroll sheet before it is paid - recompute each worker's pay from days and rates, confirm every day is charged to a real job the worker was assigned to, catch double-booked days and pass-through charges, and produce a per-job labor cost to post to job P&Ls. Use for "check payroll", "review this week's payroll sheet", "crew pay", "labor by job", or when Marcus (Dave Marcus) or Dave shares the weekly sheet.
disable-model-invocation: true
---

# Crew payroll check

Read the `c2c-context` skill first.

**Why this exists:** the weekly sheet lists date, worker, customer, job and days worked,
with mixed pay types (day rates, lump sums for a crew trip) and workers split across
several jobs in a week. Errors here mis-pay people and corrupt every job's P&L.

## Inputs

The weekly payroll sheet. Day rates and pay arrangements per worker if not on the sheet
(ask once; they are TO CONFIRM in `c2c-context` until set).

## Steps

1. **Recompute pay** per worker: days x rate, or the lump sum as stated. Show the sheet's
   number next to yours. Flag any difference.
2. **Check days:**
   - A worker cannot exceed one full day across all jobs on one date. Flag overlaps.
   - Total days per worker per week; flag over 6 or anything unusual for that worker.
3. **Check job charges:**
   - Every job named exists and is open (or closed within the pay period).
   - Allocation rule: a worker is charged to a job only for a meaningful block of time
     there, not for passing through. Flag short splits for Dave to confirm.
   - Crew leads paid a lump sum for a crew (for example a travel job): show how it splits
     across the crew and the job, and confirm no one is also paid separately for the same
     days.
4. **Payment notes:** carry over any note like "paying through <crew lead> this week" or a
   bad bank account, and list them so they get fixed, not repeated.
5. **Labor by job:** total labor cost per job for the week, ready to post to job P&Ls.

## Output

```
PAYROLL <week> - <n> workers - sheet total $<x> / recomputed $<y>
FIX BEFORE PAYING
- <worker>: <issue> (<sheet> vs <recomputed>)
CONFIRM WITH DAVE
- <worker> <date>: split <job A>/<job B> looks like pass-through
PAYMENT NOTES
- <worker>: <note>
LABOR BY JOB
- <job>: $<amt> (<days> crew-days)
```

## Rules

- Never pay, submit or edit the sheet. Report only.
- Never guess a rate. Missing rate = MISSING, ask.
- Pay information is private: show it only to the person who asked.
