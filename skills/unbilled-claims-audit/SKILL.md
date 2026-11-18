---
name: unbilled-claims-audit
description: Find insurance and job money C2C earned but never billed - pull every insurance job from a period, check whether each was actually invoiced or submitted to the carrier (by searching sent mail and billing records), and list the gaps with the evidence. Use for "unbilled claims", "did we bill everything", "audit the last 6 months of insurance jobs", "what did we forget to invoice", or "billing audit".
disable-model-invocation: true
---

# Unbilled claims audit

Read the `c2c-context` skill first.

**Why this exists:** planned in November 2026: pull all insurance jobs from the last 6 to
12 months, cross-check against what was actually sent to carriers, and flag anything with
no submission. Every hit is money already earned.

## Steps

1. **Job list.** From the CRM (and BuilderTrend for older jobs), every insurance job in the
   window: job, customer, address, carrier, claim number, status, completion date.
   Report the count and where it came from.
2. **Evidence of billing**, for each job, from any of:
   - an invoice in QuickBooks or the CRM,
   - an estimate or invoice sent to the carrier or adjuster (search sent mail for the claim
     number, then the address, then the customer last name),
   - a payment received.
3. **Classify:**
   - `BILLED + PAID`
   - `BILLED, UNPAID` -> goes to `ar-collections`
   - `NOT BILLED` - completed work, no invoice and no carrier submission found
   - `PARTIAL` - billed, but a supplement, depreciation release or final invoice is missing
   - `CAN'T TELL` - say exactly what was searched and found nothing
4. **Check your own search** before calling anything NOT BILLED: show the three searches
   run for that job. A missed search must not become a false accusation of a missed bill.

## Output

A table file (spreadsheet or markdown) with one row per job and the evidence column filled,
plus a short summary:

```
<window>: <n> insurance jobs checked
NOT BILLED: <n> - est. value <only if an estimate exists, cited>
PARTIAL: <n>
BILLED, UNPAID: <n> -> handed to ar-collections
CAN'T TELL: <n> - what would settle them
```

## Rules

- Read-only. Never contact a carrier, create an invoice or change a job from this skill.
- Every "not billed" claim carries its evidence (searches run, results). No evidence, no
  claim.
- Escrow money is not income; do not count escrow deposits as payment to C2C unless the
  record shows the transfer to operating.
