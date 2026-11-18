---
name: eli5
description: Re-explain recent work, a decision, an error, or a concept in extremely simple, non-technical language, aimed at a smart five-year-old or a 5th grader. No jargon, plain analogies instead. Trigger on "/eli5", "explain like I'm five", "explain that like I'm five", "eli5", "explain simply", "in plain english", "5th grade level", "dumb it down", or "explain it to me like a kid".
user_invocable: true
---

# ELI5

Re-tell something in the plainest possible language. This is a translation task, not a summary task: the facts stay exactly the same, only the words change.

## What to explain

- If the user names a specific thing (a PR, a ticket, an error, a file, "the thing you just did"), explain that.
- If they don't name anything, explain the most recent substantial piece of work, decision, or finding from the conversation.
- Never use this skill to explain something you haven't verified. If unsure what actually happened, check before writing (read the file, the diff, the ticket) rather than simplifying a guess.

## Rules

1. **No jargon, ever.** Every technical term gets translated into an everyday object or situation before it's used. If a technical name is unavoidable (a proper noun like a product name), say the plain-English job it does instead of the name.
2. **One consistent picture per explanation.** Pick a single everyday scene (a mailbox, a filing cabinet, a group of kids sharing a rulebook, a treasure map) and stay inside it. Don't stack three unrelated metaphors in one answer, that's more confusing than the jargon was.
3. **Short sentences. Plain words.** If a 10-year-old would need to ask what a word means, replace it.
4. **Structure:** one or two sentences setting the scene, then a short list (one idea per line) if there's more than one thing to explain, then a closing line of reassurance, what's safe, what (if anything) needs their decision, what happens next.
5. **Don't bend the truth to make the story cuter.** The analogy has to hold up if someone pushed on it. If a fix has a real caveat or risk, the plain-English version still says so, just without jargon.
6. **No em dashes.** Use commas. This applies here same as everywhere else.
7. **No emojis by default.** Only add one if the user has been using them in this conversation already, or asks for a fun version. Keep the humor in the analogy, not in decoration.
8. **Length: a short bedtime-story paragraph, not a report.** If the underlying thing is genuinely large (a whole overnight batch of work), pick the 3-5 pieces that actually matter and skip the rest rather than translating everything line by line.

## Quick glossary (translate, don't cite)

Use these as a starting point, adapt to whatever central picture you picked for this specific answer:

| Term | Plain-English idea |
|---|---|
| pull request / PR | a box of changes waiting for a yes before it goes live |
| branch | a separate copy you can safely mess with without touching the real thing |
| merge | folding that separate copy back into the real thing |
| deploy | actually turning the new version on for everyone |
| staging / production | a practice room vs. the real stage |
| migration | changing the shape of a filing cabinet's drawers |
| bug / error | something in the machine doing the wrong thing by accident |
| test | a practice run that checks the fix actually works before it counts for real |
| API / endpoint | a request window where one part of the system asks another part for something |
| cache | a sticky note with a quick answer so you don't have to look it up again |
| token / credential | a special key that proves you're allowed in |
| commit | saving a checkpoint of your work |
| revert / rollback | hitting undo back to a checkpoint that worked |

## Example

Technical: "Fixed a cross-layer PAT scope contract drift by extracting a canonical source and adding a contract test that imports the real implementations from all three consuming layers."

ELI5: "Three different parts of the app all needed to follow the same rulebook about what a key is allowed to unlock. They kept writing their own slightly different copies of the rule and not noticing when they disagreed. Now there's one official rulebook, and a little robot checks everyone's copy against it every time, so nobody can quietly get it wrong again."
