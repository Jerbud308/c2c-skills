---
name: think-deeper
description: Structured decision-thinking protocol using 6 meta mental models from Dr. Justin Sung. Invoke with /think-deeper. Use when the user needs to think through a decision, evaluate options, stress-test reasoning, or avoid cognitive blind spots. Triggers on phrases like "think deeper", "help me decide", "stress test this", "think this through", "decision framework". This is the SOLO structured framework walkthrough (one guided pass through the mental models). Good for owner-level calls: hiring, pricing, taking a big job, a vendor switch.
---

# Think Deeper

A structured thinking protocol that walks through 6 meta mental models to surface blind spots, challenge assumptions, and produce a clear decision brief.

For detailed model definitions and examples, see `references/meta-models.md`.

## How It Works

1. The user describes a problem or decision.
2. Walk through each of the 6 models interactively, one at a time.
3. After each model: ask its challenge question, tailored to the user's specific input. Wait for their response before moving on.
4. If the user says "skip" or "not relevant" for any model, move to the next.
5. After all 6 models, render a Mermaid variable map and produce a Decision Brief.
6. Offer to save the brief to their notes.

## The 6 Models (in order)

### 1. Non-Linearity Check
Surface all variables. Map their relationships. Challenge linear "if A then B" reasoning.

- Ask: "What variables are at play here? List every factor you think matters."
- Generate a Mermaid diagram of variable relationships using `mcp__claude_ai_Mermaid_Chart__validate_and_render_mermaid_diagram`.
- Challenge: "You described [X] as leading to [Y]. What other variables could influence that relationship?"

### 2. Gray Thinking Check
Find false dichotomies. Look for the spectrum between poles.

- Ask: "Are you framing this as either/or? What's the spectrum between those poles?"
- Challenge: "You said [X] vs [Y]. What does a solution look like that combines elements of both?"

### 3. Occam's Bias Check
Distinguish intentional simplification from lazy simplification.

- Ask: "What are you simplifying away? What's the black box you're choosing not to open?"
- Challenge: "You've attributed [multiple symptoms] to [single cause]. Could there be multiple contributing factors?"
- Key: Simplifying to reduce noise = good. Simplifying because you can't be bothered = dangerous.

### 4. Framing Bias Check
Question the default frame the problem was presented in.

- Ask: "How was this problem presented to you? What's a completely different way to frame it?"
- Challenge: "If you had to explain this problem to someone in a totally different industry, how would you describe it?"

### 5. Anti-Comfort Check
Attack over-confidence and unvalidated pattern matching.

- Ask: "What about your current thinking feels comfortable and familiar? What would make you wrong?"
- Challenge: "If your biggest competitor was solving this same problem, what would they do differently?"

### 6. Delayed Discomfort Check
Expose future costs of easy-path choices.

- Ask: "If you take the easy path now, what does the future cost look like?"
- Challenge: "What problem are you creating for future-you by choosing the simpler option today?"

## Output: Decision Brief

After completing all 6 models, produce this:

```
DECISION BRIEF: [Problem Title]
Date: [today's date]

VARIABLES MAP: [Mermaid diagram rendered above]

NON-LINEARITY: [Key non-linear relationships identified]
GRAY AREAS: [False dichotomies found and gray solutions proposed]
SIMPLIFICATION RISKS: [What was simplified and the known cost]
REFRAMES: [Alternative ways to see the problem]
BLIND SPOTS: [What could make the current thinking wrong]
DELAYED COSTS: [Future consequences of easy-path choices]

RECOMMENDATION: [Final synthesis -- what to do and why]
BLACK BOXES: [Areas of uncertainty that remain -- monitor these]
```

## Saving the brief

After presenting the brief, ask: "Want me to save this to your notes?"

If yes, save it as `decision-<slug>-<YYYY-MM-DD>.md` in the user's notes or shared drive folder (ask where, once, and reuse that place).

## Tone

Be a sharp thinking partner. Ask questions specific to the user's actual input, not generic prompts. Push back where the reasoning is weak. No worksheets, no hand-holding.
