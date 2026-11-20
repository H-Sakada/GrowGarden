---
name: pre-push-reviewer
description: >-
  Run a fast, read-only Gemini Flash subagent to review git changes before
  pushing to GitHub. Use whenever the user asks to review changes before
  pushing, or right before running `git push`.
---

# Pre-Push Reviewer (Gemini Flash Subagent)

Before pushing changes to GitHub, spin up a read-only Gemini Flash subagent to review the diff.

## Steps

1. Collect pending changes with `git status -s` and `git diff` (plus `git diff --staged` if staged changes exist, or `git diff origin/main..HEAD` if commits are already made).
2. Define the subagent with `define_subagent` if not already defined in this session:
   - `Name`: `pre-push-reviewer`
   - `EnableWriteTools`: `false`
   - `EnableMCPTools`: `false`
   - `EnableSubagentTools`: `false`
   - `Description`: Fast, read-only Gemini Flash code reviewer for pre-push checks.
   - `SystemPrompt`:
     > You are a fast, sharp pre-push code reviewer. Inspect the git diff and connected files before code is pushed to GitHub.
     > Check for:
     > 1. Bugs, regressions, or edge cases (cascade/specificity conflicts, broken selectors, runtime errors).
     > 2. Unintended changes or scope creep.
     > 3. Accessibility (reduced motion, focus states, semantics).
     > 4. Secrets, credentials, or leftover debug code.
     >
     > Return:
     > - **Verdict**: `PASS`, `PASS WITH NOTES`, or `BLOCK`
     > - **Findings**: ranked High / Medium / Low, plain English, with file + line references. No speculative refactors.
3. Invoke it with `invoke_subagent`:
   - `TypeName`: `pre-push-reviewer`
   - `Role`: `Pre-Push Code Reviewer (Flash)`
   - `Model`: `flash`
   - `Prompt`: Include the diff, the user's goal/constraints, and the paths of connected files to read.
4. Act on the verdict:
   - `PASS`: proceed to push.
   - `PASS WITH NOTES`: fix any real issues or share notes with the user before pushing.
   - `BLOCK`: fix blocking findings and re-message the same subagent to re-verify before pushing.
