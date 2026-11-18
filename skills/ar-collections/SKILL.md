---
name: ar-collections
description: Work C2C's accounts receivable - age every open balance, rank what to chase first, find what is blocking each one (missing paperwork, carrier holdup, customer dispute, forgotten invoice), and draft a polite, escalating follow-up sequence for approval. Use for "work the AR", "who owes us", "collections", "chase overdue invoices", "AR report", "what's collectible", or before an owner meeting on cash.
---

# AR collections

Read the `c2c-context` skill first.

**Why this exists:** C2C carries a large AR balance. Most of it is collectible without an attorney if
someone follows up steadily and with the right paperwork. That steady follow-up is what
this skill does.

## Inputs

An AR aging export (QuickBooks, CRM or spreadsheet). For each balance where available:
customer, job, invoice number and date, amount, amount paid, payer type (homeowner,
carrier, property manager, commercial), last contact, notes.

## Steps

1. **Rebuild the aging** from the source: current, 31-60, 61-90, 91-180, 180+. Show totals
   per bucket and the grand total, and check the grand total matches the source report. If
   it does not, stop and show both numbers.
2. **Classify the blocker** for each balance over 30 days:
   - `CARRIER` - waiting on insurer: supplement, reinspection, depreciation release, check
     in escrow or mortgage-company endorsement.
   - `PAPERWORK` - we owe something: completion certificate, photos, final invoice, lien
     waiver, W-9.
   - `DISPUTE` - customer disagrees with work or amount.
   - `SILENT` - no response, no known reason.
   - `UNKNOWN` - not enough notes to tell. List what to look up.
3. **Rank** by (amount x likelihood) with oldest-first as tiebreak. Likelihood: paperwork
   and carrier items are high, silent is medium, dispute is low until resolved.
4. **Draft the next touch** for the top 15, matched to the blocker:
   - Paperwork: send the missing item, then ask for payment.
   - Carrier: a status request to the adjuster with claim number and what is outstanding.
   - Silent: a friendly reminder, then a firmer one, then a call task for Phil.
   - Dispute: no collection message. Draft a note to Phil summarizing both sides.
   Sequence spacing default: day 0 email, day 3 text, day 7 call task, day 14 firm email,
   day 30 owner review. Adjust only if Phil has set a different cadence.
5. **Forgotten money:** list any job marked complete with no invoice, or an invoice never
   sent. Hand those to the `unbilled-claims-audit` skill.

## Output

```
AR <date> - total $<x> (matches source: yes/no)
<bucket totals>
CHASE THIS WEEK (top 15)
1. <customer/job> - $<amt> - <age>d - <blocker> - next: <touch> - owner: <name>
DRAFTS (approve each)
...
FOR PHIL TO DECIDE
- disputes, anything 180+ days, anything he might send to an attorney
```

## Rules

- Never send. Phil approves each message or the sequence template once, in writing.
- Homeowner balances are consumer debts. Messages stay polite, factual, sent at reasonable
  local hours, never threaten action C2C has not decided to take, and never discuss the
  debt with anyone but the customer or their authorized rep. Have counsel review the
  sequence templates once before first use.
- Never change a balance or write anything off. Flag it for Phil.
