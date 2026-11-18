---
name: handoff
description: Produce an exhaustive, self-contained handoff so a fresh agent can resume work cold, with zero access to the current conversation. Use when banking unfinished work, running low on usage limits, ending a session mid-task, or when the user says "hand this off", "bank it", "write this up for the next agent", or "make a ticket I can point an agent at".
user_invocable: true
---

# Handoff

Write the document you would want if you woke up tomorrow with amnesia and had to finish
this work today.

**The reader has NONE of your context.** No conversation, no scrollback, no memory of what
was tried. Every assumption living only in your head right now is lost unless you write it
down. Assume they will act on this document literally.

## Where it goes

1. **A markdown file** holding the full context. Put it next to the work it describes
   (the repo, the memory dir, the project folder), never in a temp dir. Name it
   `HANDOFF-<slug>-<YYYY-MM-DD>.md`. Commit it if the location is a git repo.
2. **Optionally, a short card** on whatever board the team uses (the CRM task list, a
   Kanban card) whose description is a two-line summary plus the file path. The file is
   the payload. Ask the user for priority if they have not said. Do not guess.
3. Report the file path (and card link, if made) back to the user.

## Capture state mechanically, not from memory

Before writing, RUN the commands and paste real output. Do not recall numbers, measure
them. Sizes, counts, commit hashes, ticket states, branch divergence, test results.

A `0` or an empty result is a crash signature as often as it is a real value. Re-check
any surprising number a second way before writing it down.

## Required sections

Include every one that applies. Omit a section only if it is genuinely empty.

1. **Why this exists.** The problem in plain language, and the user's actual words about
   why it matters. Motivation is the first thing lost and the hardest to reconstruct.
2. **The verified diagnosis.** What is actually true, with the evidence that proved it.
   Mark anything unverified as unverified.
3. **What was REJECTED and why.** The highest-value section and the one people skip.
   Without it the next agent rebuilds the thing you already killed. Give the reasons, not
   just the verdict.
4. **Corrections: claims that were disproven.** Anything believed mid-session and later
   falsified. This stops the next agent re-deriving a dead end, and stops them trusting a
   stale claim from an earlier note.
5. **The approved plan**, and the **first move** concretely enough to start in one step.
6. **Current state with real numbers.** Sizes, counts, recent commit hashes, what is
   committed vs uncommitted, and the exact command to recover the prior state.
7. **Open decisions that belong to the USER, not the agent.** Say plainly what must not be
   decided unilaterally, and what the recommendation on record is.
8. **Unrelated live issues discovered along the way.** With severity, evidence, and
   whether they are already deferred by a human decision.
9. **Landmines.** Tool traps, false greens, wrong-guess patterns. Each with the concrete
   symptom, so it is recognizable rather than abstract.
10. **Verification commands that actually worked.** Copy-pasteable. This is what turns a
    two-hour re-orientation into ten minutes.
11. **Definition of done.** A checkbox list, including explicit "do NOT build X" items
    where scope creep is the risk.

## Rules

- **Never fabricate.** No invented ticket IDs, paths, URLs, or command output. If you do
  not know, write "UNVERIFIED" or "unknown, would need X to determine."
- **Distinguish proven from assumed** on every load-bearing claim.
- **Preserve the user's decisions verbatim**, especially deferrals and refusals. "Phil
  deferred this on <date> until X" prevents an agent from helpfully undoing a choice.
- **Record near-misses and your own errors.** A handoff that hides mistakes hands over the
  same mistakes. If a review caught defects in your work, say what they were.
- **Sweep for siblings before you write.** If you fixed one instance of a bug class, say
  explicitly whether you checked for others. Unswept siblings are a documented repeat
  failure; naming the gap is mandatory even when you did not close it.
- **Commit any uncommitted work first**, or the handoff describes state that no longer
  exists. Flag anything you deliberately left uncommitted and why.
- Length is not the goal, completeness is. Do not pad, but never drop context to be brief.
