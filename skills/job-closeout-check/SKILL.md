---
name: job-closeout-check
description: Check that a C2C job is complete on paper before it is closed or final-billed - receipts, sub bills, labor, photos, permits, signed paperwork, final invoice and supplements all present, and the job P&L adds up. Use for "can we close this job", "close-out check", "is the P&L complete", "what's missing on <job>", "final billing check", or weekly across all jobs marked complete.
---

# Job close-out check

Read the `c2c-context` skill first.

**Why this exists:** job P&Ls have been incomplete because receipts and sub bills were never
uploaded, so a job can look profitable and not be. The new field app posts receipts
straight to the job; this check catches what still slips through.

## Checklist (per job)

| Item | Where to look | Pass when |
|---|---|---|
| Contract / work authorization signed | CRM documents | signed copy attached |
| Permit opened and closed (if required) | CRM, Jodi | final inspection passed |
| Before / during / after photos | CompanyCam | all three phases present |
| Material receipts | CRM job receipts | count matches purchases, or Dave confirms none |
| Sub invoices | CRM, QuickBooks | every sub on the job has a bill |
| Labor | payroll by job | crew-days posted |
| Estimate vs. final scope | Xactimate / CRM | differences explained or supplemented |
| Supplements (insurance jobs) | carrier correspondence | submitted, and approved or denied |
| Completion certificate / customer sign-off | CRM documents | signed |
| Final invoice | QuickBooks / CRM | sent, with date |
| Lien waivers from subs (if used) | CRM documents | present for each sub paid |

## Steps

1. Run the checklist; mark each item PASS, MISSING or N/A with the source.
2. **P&L sanity:** revenue billed minus materials, subs and labor. Flag a margin that is
   unusually high (often a sign of missing costs) or negative.
3. List missing items with the person who owns each (from `c2c-context`).

## Output

```
<job> - <customer> - READY TO CLOSE / NOT READY
MISSING
- <item> - owner: <name>
P&L: revenue $<x> - materials $<a> - subs $<b> - labor $<c> = $<margin> (<pct>%) <flag>
```

## Rules

- Read-only. Never close a job, send an invoice or change records.
- A margin is only as good as its inputs: say which cost lines are empty.
