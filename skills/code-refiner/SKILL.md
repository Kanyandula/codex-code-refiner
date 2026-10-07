---
name: code-refiner
description: Review recently changed code and apply behavior-preserving refinements when the user asks to simplify code, clean up an implementation, or reduce complexity.
---

# Code Refiner

Perform a focused cleanup pass on code the user identifies or has recently changed. This is an editing skill: apply clear improvements instead of returning only a list of suggestions. Keep the behavior intact and the changes limited to the cleanup requested.

Use this skill when the user invokes `$code-refiner` or clearly requests a cleanup pass, such as “simplify this code,” “clean up my changes,” or “reduce the complexity here.” Do not assume every implementation task should be followed by a cleanup pass.

## Choose the review scope

- If the user gives a file, directory, branch, or PR target, use that target and follow the repository's available context for it.
- Otherwise, inspect the current task's changes. In a Git repository, review the staged and unstaged diff and check `git status` for relevant untracked files. Use conversation context to identify the code just implemented or changed.
- In a non-Git workspace, use the files named by the user or changed in the current task.
- Read applicable project guidance and nearby code before editing. Follow the project's existing style and patterns.
- Keep the pass focused on touched code and the immediately related code needed to understand it. Expand scope only when the user asks.
- If the target cannot be determined safely, ask one concise question before editing.

## Review and fix

Inspect the target through these lenses:

1. **Reuse:** Prefer established project helpers and existing patterns over duplicated logic or a new helper that adds no useful boundary.
2. **Clarity:** Reduce needless nesting, branching, repetition, indirection, and misleading names. Prefer explicit readable code over dense one-liners or fewer lines for their own sake.
3. **Efficiency:** Fix clear, material inefficiencies such as repeated work or unnecessary allocations. Avoid speculative micro-optimizations.
4. **Abstraction:** Check whether the code has the right level of abstraction. Remove unnecessary layers, but preserve boundaries that make responsibilities clear or make the code easier to change.

Apply a fix when it is a clear improvement and its behavior is straightforward to preserve. If the code is already clear, leave it alone. If a possible improvement depends on uncertain behavior or project assumptions, do not guess; report the opportunity and what needs clarification.

Preserve observable behavior, including public interfaces, return values, error behavior, validation, authorization checks, ordering, concurrency, persistence effects, logging, and edge cases. Do not remove defensive code or compatibility handling merely to make the implementation shorter. Avoid unrelated formatting and opportunistic refactors.

This skill focuses on cleanup, not a general correctness or security review. If a separate bug or security concern becomes apparent, identify it briefly as a separate finding; do not silently broaden the cleanup into a different task.

## Finish

- Inspect the final diff and remove accidental or unrelated edits.
- Follow the active session and project instructions for verification. State what was and was not checked; never imply that behavior was tested when it was not.
- Summarize the cleanup fixes made and any significant opportunity left unchanged because its behavior or value was uncertain. Keep the summary brief.
