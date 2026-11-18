---
name: cold-read
description: "Make a spec, plan, PRD or handoff executable by a cheaper model in a fresh session, then prove it: a Sonnet-level agent reads it cold and lists every point where it would have to guess, you fix those, and repeat until no blockers remain. Use whenever a spec or plan will be run by a headless, stateless or less capable agent (Sonnet, Haiku, a new session, an overnight run, a subagent), when the user says 'a less intelligent model should get the same result', 'make the spec bulletproof', 'cold read', 'can Sonnet run this', or before handing any build doc to an overnight run or a new session. Also invocable as /cold-read <path>."
---

# Cold read

Opus writes the spec once; a cheaper model executes it many times. A spec is ready when the cheaper model, with no access to the conversation that produced it, would not have to guess anywhere. That cannot be judged by the author, who fills gaps from memory without noticing. So the check is mechanical: a target-model agent reads it cold and reports its guesses.

This is an executability test, not a design review. For "is this the right design / are there bugs or UX gaps", use `/triage`. Run both on high-stakes specs: `/triage` first, cold-read last.

## Inputs

- The document path (argument, or the spec just written in this session).
- Target executor: default `sonnet`. Use `haiku` if the run will use Haiku.
- If invoked with no document, write the spec first using section 1, then run section 2.

## 1. Write it to be executed, not read

Every item below closed a real gap that a cold reader found. Check each one before the first cold read; it saves a round.

- **Kickoff prompt, verbatim, at the top.** The exact text to paste into the new session: role, files to read first, process, stop rules.
- **Precedence.** "Where this spec and any other doc disagree, this spec wins." Say which inputs are optional reference.
- **Exact file tree** and which phase creates each file. Nothing used before the phase that builds it (a CLI needed in phase 1 must be built in phase 0).
- **Config files with every field, default, allowed values and validation rule**, including which empty values are legal in which mode. Committed defaults must load.
- **Env var names and where each value comes from.** Never values.
- **Function signatures** for every module boundary, including return shapes and every outcome value (a missing `skipped` outcome stalled a loop).
- **External APIs verified live, never from memory.** Fetch the vendor's reference page or schema (e.g. Apify actor build `inputSchema`, an `llms.txt`), record field names and the date. Mark anything unverified as provisional, name the constant that holds it, and add a phase-1 check that records the real value.
- **Every state has a setter.** For each status enum, name what sets each value and what moves it on. A status nothing sets (`done`) or nothing clears is a gap.
- **One ordering per selection.** Two sentences giving different sort orders for the same queue is a forced guess.
- **Null semantics.** "Empty" must say NULL, `''` or `'[]'`.
- **Failure path for every external call:** retry rule, what is written on final failure, when to give up (a counter and a threshold), so nothing retries forever.
- **One-shot guards vs rehearsal.** If something may happen only once (a UNIQUE key, "never twice"), say whether a dry run consumes it and how to reset rehearsal state.
- **Gates that can actually be passed.** If acceptance needs an approval, a UI or data that a later phase builds, give the interim command (e.g. the SQL that approves rehearsal rows).
- **Acceptance is a command plus an expected output.** `grep -c X file` returns at least 1, `agreement >= 90`, an exit code. Never "the reviewer has read it" without an artifact to compare against.
- **Data invariants survive cleanup.** If retention deletes rows, check that every reconciliation identity still holds afterwards.
- **Paths are absolute or derived from one root**, so tests can point at a temp dir and never touch real data (a test that writes the real kill file blocks production).
- **Time and timezone defined once:** what "today" means, and what is scheduled by whom (manual, cron, launchd).
- **Who does what.** Roles (orchestrator, builder model, reviewer model), who runs network and live commands, who commits which artifacts, who never pushes or merges.
- **Fixtures plan.** Who captures real responses, how they are sanitized, what builders synthesize, and how synthetic fixtures are flagged.
- **Stop-and-ask list.** Credentials, first live or irreversible action, any change to safety settings, schema mismatches, anything touching a real person's or client's account.
- **The environment as it is.** Runtime version actually installed, how to select the right one, which keys already exist on the machine. Check these, do not assume.

## 2. The cold-read loop

1. Make the spec durable on disk first.
2. Spawn ONE agent: `subagent_type: general-purpose`, `model: <target>`, foreground. Prompt, verbatim apart from the paths:

```
You are about to be the orchestrator of a build from a spec, starting cold. Before anyone builds, we need to
know where the spec would force you to guess.

Read <SPEC PATH> completely, plus <OTHER INPUT PATHS>. Do not write or change any files. Do not make network calls.

Task: list every point where, executing this spec exactly, you would have to guess, make an unstated decision,
or stop because information is missing or contradictory. For each item give: the section number, the exact
sentence or field, what you would have to guess, and the smallest addition to the spec that would remove the guess.

Rules:
- Only list real execution blockers or forced guesses. Do not give opinions on the design, the product, style,
  or risk. Do not suggest features.
- Check internal consistency: field names used in one section that are defined differently in another, steps
  that reference things never defined, acceptance items that can't be measured with the given commands,
  ordering problems between phases.
- Rank items: BLOCKER (cannot proceed), GUESS (would proceed but likely differently from what the author
  intended), MINOR.
- Be concise. Return at most 25 items.
```

3. **Triage.** Verify each item against the spec yourself (the reader is sometimes wrong; it also verifies the environment, e.g. installed Node version, so take those checks seriously). Fix every BLOCKER and GUESS by editing the spec, not by arguing. Fix MINOR if it costs one line. Never fix by adding a design the user did not ask for; pick the smallest rule that removes the guess.
4. **Round 2: the same agent**, via `SendMessage` to its agent id (it keeps its context, so it checks its own items):

```
The spec has been revised to address your items. Re-read <SPEC PATH> in full (do not rely on memory of the old
version; still no file changes, no network). Two jobs: 1. For each of your items, say RESOLVED or STILL OPEN (one
line each; if still open, quote what's missing). 2. Any NEW forced guess or contradiction the revisions introduced,
same format as before, ranked BLOCKER/GUESS/MINOR. Max 15 new items. Same rules: execution blockers and forced
guesses only, no design opinions.
```

5. **Round 3, blockers only**, same agent: "Reply only with each item RESOLVED or STILL OPEN, then any NEW BLOCKER the edits introduced (max 5)." Fixes introduce new gaps; in the first run of this skill, round 2 found 13 new items and round 3 found 4 new blockers.
6. **Stop** when a round returns zero blockers, or after round 3. If blockers remain after round 3, fix them and tell the user which ones were fixed without a re-read.

Cost: one agent, three short turns. Do not fan out several readers; one reader with memory of its own findings converges faster.

## 3. Report

Six lines max: the path, items found per round (e.g. "25, then 13, then 4 blockers, all fixed"), anything still open, and what the user must supply before execution. The findings themselves stay in the agent output, not in chat.

## Provenance

Built 2026-10-23 by RAC Projects AI on an internal spec written by Opus for a headless Sonnet build; three cold-read rounds found 25, 13 and 4 items.
