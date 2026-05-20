# AGENTS.md

## Goal

Use Codex as an implementation agent that can self-review and refine work before a human merge.

Every task should move through this workflow:

```text
Goal -> Plan -> Implement -> Skill Review -> Refine -> Test -> Final Summary
```

## Default Codex Workflow

For every issue, prompt, or PR task:

1. Restate the goal in one or two lines.
2. Identify the smallest safe change that satisfies the goal.
3. Create a short plan before editing.
4. Implement the change.
5. Run the relevant checks.
6. Review the change using the reviewer prompts in `.codex/reviewers/`.
7. Refine the implementation based on reviewer feedback.
8. Repeat review/refine until there are no critical or high-risk findings.
9. Final response must include:
   - What changed
   - Files changed
   - Checks run
   - Reviewer findings
   - Remaining risks

## Reviewer Skills

Use these reviewer prompts when relevant:

- `.codex/reviewers/requirements.md`
- `.codex/reviewers/backend.md`
- `.codex/reviewers/security.md`
- `.codex/reviewers/testing.md`
- `.codex/reviewers/maintainability.md`

## Hard Rules

- Do not claim tests passed unless they were actually run.
- Do not hide failing checks.
- Prefer small, reversible changes.
- Avoid unrelated refactors.
- Keep final merge human-approved.
- If requirements are unclear, make a safe assumption and document it.

## .NET / Backend Preferences

When this repository contains .NET backend code:

- Prefer dependency injection over hard-coded dependencies.
- Prefer async/await for I/O.
- Keep business logic testable outside controllers.
- Validate external input at boundaries.
- Avoid logging secrets or personal data.
- Add or update unit tests for behavior changes.
