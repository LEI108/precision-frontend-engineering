---
name: precision-frontend-engineering
description: Apply precise, evidence-led frontend engineering practices when extending or refining an existing application, with surgical changes, maintainable contracts, deliberate reuse, and focused verification.
---

# Precision Frontend Engineering

Use this skill for non-trivial frontend work in an existing repository: feature additions, API integration, UI refinement, component reuse, and focused maintenance. It complements higher-priority project instructions, `lean-code-edits`, visual-design skills, and framework-specific guidance; it does not replace them.

## Operating principles

- Establish the requested stage before acting: analysis, proposed patch, implementation, static check, runtime check, or visual acceptance.
- Inspect the current checkout, route/data path, relevant callers, and worktree diff before changing code. Treat restored, stashed, or uncommitted work as user-owned.
- Make the smallest change that satisfies the confirmed requirement. Preserve existing behavior, wording, assets, styles, and public contracts unless the task explicitly changes them.
- Prefer source-level reuse when behavior and ownership are genuinely shared. Do not extract or generalize code solely because two screens look similar.
- Keep backend facts, frontend assumptions, development mocks, and derived presentation values distinguishable.
- Use UTF-8 for inspection and edits; prefer bounded patches over whole-file rewrites.
- Verify the changed boundary at the level the task requires. Never turn a lint/build result into a runtime, backend, or visual-acceptance claim.

## Workflow

1. Confirm scope, authorization, affected routes, data ownership, and unresolved contract decisions.
2. Inspect the repository and current diff; trace the rendering, navigation, and data paths before selecting an edit point.
3. Build a short change map: files, anchors, preserved behavior, new behavior, and the smallest verification for each risk.
4. Implement in local, reviewable patches. Remove only imports, state, or helpers orphaned by the same change.
5. Check comments, selectors, response handling, loading/empty/error states, and mock boundaries while the context is fresh.
6. Run focused checks and report their exact boundaries, including anything not verified.

## Read references selectively

- For worktree safety, surgical edits, and change maps, read [references/change-safety-and-scope.md](references/change-safety-and-scope.md).
- For API wrappers, response handling, contract gaps, and mocks, read [references/api-contracts-and-mocks.md](references/api-contracts-and-mocks.md).
- For component extraction, page composition, and reuse decisions, read [references/component-reuse-and-boundaries.md](references/component-reuse-and-boundaries.md).
- For comments and copyable handoffs, read [references/comments-and-handoff.md](references/comments-and-handoff.md).
- For CSS/runtime selectors and proportionate checks, read [references/focused-verification.md](references/focused-verification.md).

Read only the references relevant to the current task; do not load them as a generic checklist when the task is trivial.
