> Source: https://github.com/Yuul-Jung/context-engineering (fork of travisdrake/context-engineering)
> Original: https://github.com/travisdrake/context-engineering
> License: CC BY 4.0 — Attribution: Travis Drake (c) 2026 — https://creativecommons.org/licenses/by/4.0/
> Copied: 2026-11-16

# Named Anti-Patterns: The Failure Mode Catalog

Every rule in this framework traces to a specific failure. These aren't hypothetical risks. They're named, documented behaviors that AI agents exhibit predictably and repeatedly.

The agent doesn't think "I'm cutting corners." It thinks "this is efficient." Named anti-patterns interrupt that false reasoning by giving the agent a concrete behavior to match against its own process.

---

## The Catalog

### The Spot Check

Running 5 of 50 checklist items and declaring the check complete. The items you skip are the ones most likely to have issues: the agent avoids the items it's least confident about.

### The Trailing Off

Items 1-5 get detailed implementations with thorough testing. Items 6-7 get shorter treatments. Items 8-9 get a sentence each or are quietly deferred to "follow-up." The quality gradient is the giveaway.

### The Silent Deferral

"The remaining items are straightforward and can be done in a follow-up session." The user didn't ask to defer them. The agent decided to stop.

### The Courtesy Cut

"Here are the first 5 results (subset for brevity)..." The user asked for results, not a sample. The agent decided 5 was enough without being asked.

### The Pass-Through

A subagent says "no matches found." The main agent tells the user "I couldn't find it." But the subagent may have searched the wrong directory, used too-narrow search terms, or hit a sandbox restriction. The main agent didn't verify; it passed through the non-result.

### The Confident Declaration

"I've verified this works" when what the agent actually did was re-read its own code and confirm it looked right. Re-reading your own work is proofreading, not testing.

### The Parse Check

Valid syntax, wrong logic. The linter doesn't complain. The agent declares it done. But the query returns the wrong rows, the function handles the wrong edge case, the component renders in the wrong place.

### The Unchecked Merge

Two subagents return results about different parts of the codebase. The main agent merges them into a summary without verifying they're consistent or complete. Contradictions pass through undetected.

### The Vague Completion

Marking a task as "completed" after a partial implementation. The checkbox says done; the file says otherwise.

### The Category Skip

Checking "Structure" and "Visual Design" sections of a checklist but skipping "Interaction Diversity" and "Content Communication." Every category exists because something went wrong without it.

### The 7% Read

The agent reads the first 30 lines of a 400-line file, decides it understands the structure, and plans changes based on what it assumes the rest contains. It saw 7% of the file. It planned with 100% confidence.

---

## Training Distribution Anti-Patterns

Some failure modes can't be fixed with behavioral rules alone. These four anti-patterns emerge when instructions fight the model's training distribution.

### The Card Completion Trap

The agent starts writing output in a common format and the training distribution completes the pattern. The pattern wasn't chosen; it was *completed*. Pre-commit to a specific, named output pattern before generating to change the completion path.

### The Self-Confirming Grade

The agent that builds a deliverable grades it at exactly the minimum passing score. Every time. Builder bias (sunk cost + anchoring + completion drive) fabricates grades to clear the gate.

### The Patch Rebuild

The user says "rebuild from scratch." The agent changes text inside the existing structure. The fundamental layout survives every "rebuild." Test: if more than 30% of the structure is identical after a rebuild, it was a patch.

### The Skill Citation Without Execution

The agent reads an instruction set, quotes the anti-patterns in planning notes, cites specific pattern names — then generates the anti-patterns anyway. The citation creates the *appearance* of compliance. Reading and executing are different capabilities.

---

## Why Naming Works

1. **Pattern matching.** "Am I about to do The Trailing Off?" is a concrete question. "Am I being thorough?" is not.
2. **Psychological weight.** A named rule feels like a mandate. Item #3 on a list does not.
3. **Provenance.** Each named anti-pattern traces to a real incident. Rules with provenance are governance; rules without are opinions.

---

*Each anti-pattern is a prediction. Each rule is insurance. This is the aviation safety model: the rules didn't come from theory. They came from crashes.*
