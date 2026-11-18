---
name: sub-invoice-intake
description: Turn subcontractor and vendor invoices (PDF, photo, or email) into checked, job-matched entries ready for approval and QuickBooks - extracting vendor, amount, job, line items and dates, catching duplicates and math errors, and routing each to the right approver. Use for "process these invoices", "sub invoices", "what's in the invoice queue", "match this bill to a job", or when an invoice arrives in any C2C inbox.
---

# Sub invoice intake

Read the `c2c-context` skill first.

**Why this exists:** sub invoices used to go through several inboxes, a VA, Excel and
BuilderTrend before anyone approved them, and job P&Ls stayed incomplete because bills
never got attached. One queue, checked once, fixes both.

## Steps

1. **Extract** from each invoice: vendor, invoice number, invoice date, due date, job or
   address or PO referenced, line items (description, qty, rate, amount), subtotal, tax,
   total, payment terms, remit-to. Cite the page or line. Anything unreadable is `MISSING`.
2. **Check:**
   - Math: line items add to subtotal; subtotal + tax = total.
   - Duplicate: same vendor + invoice number, or same vendor + amount within 30 days.
   - Job match: the job exists, is open, and the vendor is on that job. If not, flag.
   - Scope: line items look like work that job needs (a roofing sub billing plumbing gets
     a flag, not a rejection).
   - Over budget: if the job's budget or estimate is available, show this invoice's share.
3. **Route** using the approval rule in `c2c-context`. If that rule is still TO CONFIRM,
   route everything to Phil and Dave and say the rule is not set.
4. **Prepare the QuickBooks entry** as a draft only: vendor, bill date, due date, account
   or class, job, amount, memo with invoice number. Do not post it.

## Output

```
INVOICE QUEUE - <n> invoices - $<total from the documents>
READY TO APPROVE (<n>)
- <vendor> #<inv> - <job> - $<amt> - approver: <name>
NEEDS A LOOK (<n>)
- <vendor> #<inv> - <problem: duplicate / math off by $x / no job match / scope>
QUICKBOOKS DRAFTS
- <one block per approved invoice>
```

## Rules

- Never post to QuickBooks or pay anything. A named approver approves each invoice.
- Never change an amount to make the math work; flag the gap.
- Treat a change of remit-to bank details on a known vendor as a fraud flag and tell Phil
  to confirm by phone with a number already on file, not one from the email.
