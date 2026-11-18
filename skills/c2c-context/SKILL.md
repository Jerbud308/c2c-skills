---
name: c2c-context
description: Company context for C2C Restoration (who does what, which systems hold which data, approval rules, and the hard rules every C2C agent follows). Read this first before running any other C2C skill, and whenever a task mentions a C2C person, job, claim, carrier, invoice, lead, crew or inbox.
user-invocable: false
---

# C2C context

Every C2C skill reads this file first. Anything marked **TO CONFIRM** is a blank Andy fills
in with the owner before the skill that needs it goes live. Never guess a TO CONFIRM value;
ask the user and suggest they update this file.

## The business

C2C Restoration: roofing, restoration and insurance-claim work, residential and commercial
(including commercial roofing maintenance). Insurance job funds flow through escrow; only
the PA fee and the expenses moved to the operating account show up in QuickBooks.

## People and lanes

Names: "Jodi" is spelled with an i. "Marcus" always means Dave Marcus, never Dave the owner;
if a message says only "Dave", it means the owner, and if that is unclear, ask.

| Person | Lane | What they need from an agent |
|---|---|---|
| Blake (owner) | Storm and inbound lead intake, sales. Kept in the loop on compliance. | Fast lead triage, first-touch drafts, a short callback list, mobile-friendly answers. |
| Phil (owner) | Roofing operations and the financial workflow: ProLine, QuickBooks, signed contracts, scheduling, inbox triage. | Inbox sorted into job activity, AR and billing follow-up, invoice approvals, one clean daily brief. |
| Dave (owner) | Job and field-to-finance operations: moving the team off BuilderTrend onto the C2C CRM, subcontractor invoices, job P&L. | Invoice intake and routing, job close-out checks, payroll checks, the same actions on phone and desktop. |
| Andy (embedded AI consultant) | Builds and runs the CRM, AIOS, integrations (QuickBooks, CompanyCam, Twilio), onboarding, data migration, AR work. | Build discipline, handoffs, specs a cheaper model can run, skill authoring. |
| Jodi | Permits, compliance and licensing (renewals, insurance, training flags); routes compliance to Blake. | Permit and license status pulled out of email, renewal dates surfaced early, compliance items routed to Blake. |
| Stephanie | Reputation and marketing; manages Phil's inbox and some roofing ops. | |
| Dave Marcus (goes by "Marcus") | Weekly crew payroll spreadsheet: days, rates and job allocation per worker. | The payroll sheet checked before it is paid, and labor cost per job. |

## Systems (where the truth lives)

| Data | System |
|---|---|
| Leads, jobs, job activity, receipts, job P&L, service contracts, maintenance requests | C2C CRM (C2C HQ) |
| Legacy job data during the transition | BuilderTrend (being retired) |
| Roofing CRM | ProLine |
| Operating expenses, invoices, payments | QuickBooks |
| Dry-out and claim estimates | Xactimate (in-house) |
| Job photos | CompanyCam |
| Texts to leads and customers | Twilio through the CRM |
| Email | Several company inboxes; one person can own up to four. Inbox list: **TO CONFIRM** |

## Rules and thresholds

- Subcontractor invoice approval: who approves, and the dollar amount under which Dave can
  push an approved invoice straight to QuickBooks: **TO CONFIRM** (proposed, not decided).
- Payroll allocation: a crew member is billed to a job only when assigned there for a
  meaningful block of time, not for passing through. Day rates and the minimum block:
  **TO CONFIRM** with Marcus.
- Signed-contract alerts go to Phil, not to every manager.
- Collections: who signs off on a collections sequence before first use, and when an account
  goes to an attorney: **TO CONFIRM** with Phil.

## Hard rules for every C2C agent

1. **Draft, never send.** No email, text, invoice, payment or QuickBooks entry leaves without
   a named person approving that exact item. "Go ahead" on a batch means show the batch first.
2. **Never invent a number.** Amounts, dates, claim numbers, policy numbers and carrier names
   come from a source document or system, cited. If it is missing, write MISSING and ask.
3. **Customer and claim data stays inside C2C systems.** Do not paste it into outside tools,
   public sites or personal accounts.
4. **Name the owner.** Every flagged item ends with who acts on it, from the table above.
5. **Short by default.** Owners read on a phone between jobs: answer first, five lines or
   fewer, details only on request.
