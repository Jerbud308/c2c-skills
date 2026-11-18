---
name: carrier-supplement-draft
description: Draft an insurance supplement request for a C2C job - comparing the carrier's approved estimate to C2C's Xactimate scope, listing each missing or under-paid line item with the photo, measurement, code requirement or field note that supports it, and writing the cover letter to the adjuster for approval. Use for "write a supplement", "carrier short-paid this job", "compare the carrier estimate to ours", "what did the adjuster miss", or "supplement for <claim>".
---

# Carrier supplement draft

Read the `c2c-context` skill first.

**Status: suggested, confirm with Phil before use.** Built from the fact that C2C writes
its Xactimate estimates in-house and works insurance claims; the exact supplement process
(who writes them, format the carriers expect) is not yet documented.

## Inputs

- The carrier's estimate (PDF) and C2C's Xactimate estimate (PDF or export).
- Job photos (CompanyCam), measurements, field notes, and any code or manufacturer
  requirement the scope relies on.
- Claim number, carrier, adjuster name and email.

## Steps

1. **Line up the two estimates** by trade and line item. For each difference, classify:
   `MISSING` (not on carrier estimate), `UNDER` (quantity or price lower),
   `DIFFERENT` (different item or method), `OK`.
2. **Support each MISSING / UNDER line** with evidence: photo file name, measurement,
   field note, or the code or manufacturer requirement (cite the exact section; if you
   cannot cite it, write "needs citation" instead of naming one).
3. **Drop weak items.** If a line has no evidence, list it under "not requesting yet" with
   what evidence would support it. A supplement with unsupported lines hurts the strong ones.
4. **Total** the requested difference from the line items. Do not round or estimate.
5. **Draft the cover letter** to the adjuster: claim number, property, a one-paragraph
   summary, the line-item table, attachments list, and a polite ask for review by a date.

## Output

A supplement file (table + letter) and a summary:

```
<claim> - <carrier> - requesting $<total> across <n> items
STRONG (<n>): <items>
NOT REQUESTING YET (<n>): <items> - need: <evidence>
```

## Rules

- Never send to the carrier. Phil (or whoever owns estimating) approves it.
- Never alter photos or measurements, and never claim damage the evidence does not show.
