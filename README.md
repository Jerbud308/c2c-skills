# C2C skill packet

Skills for C2C Restoration's owners (Blake, Phil, Dave), Jodi (permits and compliance), Marcus (Dave Marcus, payroll) and Andy, built from what they
actually do day to day (2026-10 and 2026-11 meeting notes). 20 skills: 12 new C2C ones,
8 ported from our library. Extras that help but aren't core are in [NICE-TO-HAVE.md](NICE-TO-HAVE.md) (5 ready in `nice-to-have/`).

## Fastest install (onsite)

Mac / Linux:
```
git clone https://github.com/Jerbud308/c2c-skills.git && mkdir -p ~/.claude/skills && cp -R c2c-skills/skills/* ~/.claude/skills/
```
Windows (PowerShell):
```
git clone https://github.com/Jerbud308/c2c-skills.git; New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null; Copy-Item -Recurse -Force c2c-skills\skills\* "$env:USERPROFILE\.claude\skills\"
```
Then restart Claude Code. To install only one person's set, copy just the folders in their column below.

## Who gets what

| Skill | Blake | Phil | Dave | Jodi | Marcus | Andy | Invocation | Typical trigger |
|---|:-:|:-:|:-:|:-:|:-:|:-:|---|---|
| c2c-context | x | x | x | x | x | x | Agent only | Loaded by every C2C skill. Andy fills the TO CONFIRM blanks first. |
| c2c-morning-brief | x | x | x | x | x |   | Both | Typed, or a scheduled routine each morning |
| lead-triage | x |   |   |   |   |   | Both | "what leads do I call today" |
| inbox-to-job |   | x |   | x |   |   | Both | "go through my inbox" |
| sub-invoice-intake |   | x | x |   |   |   | Both | Typed, or chained from inbox-to-job |
| ar-collections |   | x |   |   |   | x | Both | "work the AR" |
| unbilled-claims-audit |   | x |   |   |   | x | Human only | `/unbilled-claims-audit` (heavy, read-only sweep) |
| crew-payroll-check |   |   | x |   | x |   | Human only | `/crew-payroll-check` (private pay data) |
| job-closeout-check |   |   | x | x |   |   | Both | "can we close this job" |
| carrier-supplement-draft |   | x |   |   |   |   | Both | Suggested; confirm the process with Phil first |
| job-meeting-prep | x | x | x |   |   |   | Both | "prep me for the adjuster meeting" |
| meeting-to-tasks | x | x | x | x | x | x | Both | After any meeting |
| think-deeper | x | x | x |   |   |   | Both | Big owner decisions |
| eli5 | x | x | x | x | x |   | Both | "explain that simply" |
| voice-match | x | x | x | x |   |   | Both | Once per person, so drafts sound like them |
| writing-style |   |   |   |   |   | x | Agent only | Applied to written output automatically |
| handoff |   |   |   |   |   | x | Both | End of a work session |
| cold-read |   |   |   |   |   | x | Both | Before handing a spec to a cheaper model |
| test |   |   |   |   |   | x | Both | "does this work" |
| unlazy |   |   |   |   |   | x | Both | Long builds that stall at 80% |

**Invocation:** Both = Claude picks it from the description and the user can type `/name`.
Agent only = hidden from the `/` menu. Human only = runs only when typed.

## Install (scope)

- **Global, per person (recommended):** copy each folder in `skills/` into
  `~/.claude/skills/` on that person's machine (Windows: `%USERPROFILE%\.claude\skills\`).
  Works in every project. Copy only that person's column plus `c2c-context`.
- **Project, shared:** put `skills/` in the C2C repo at `.claude/skills/` so everyone working
  in that repo gets the same set, versioned in git. Good for Andy's skills.
- **Claude.ai / desktop app:** zip each skill folder and upload it under Settings,
  Capabilities, Skills. Note the `disable-model-invocation` and `user-invocable` flags are
  Claude Code settings and may be ignored there.

## Before go-live (Andy)

1. Fill every **TO CONFIRM** in `skills/c2c-context/SKILL.md` with the owners: inbox list,
   invoice approval rule and threshold, crew day rates and the allocation minimum,
   collections sign-off.
2. Fill Jodi's and Marcus's lanes the same way (permit list, renewal calendar; worker roster and rates).
3. Have counsel review the `ar-collections` message templates once.
4. Run each skill on one real past example with the owner watching before relying on it.

## Hard rule baked into every skill

Draft, never send. Nothing goes to a customer, carrier, sub, QuickBooks or the CRM without
a named person approving that item.

## Built from

Meetings 2026-10-22 (scope, AR, Xactimate in-house), 2026-11-09 (CRM rollout, Dave
first off BuilderTrend), 2026-11-11 (inbox owners, 24 leads stuck, payroll sheet),
2026-11-12 (field receipts, unbilled-claims audit). Facts not found in those notes are
marked TO CONFIRM rather than guessed.
