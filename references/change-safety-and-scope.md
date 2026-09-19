# Change safety and scope

Use this reference before editing an existing repository or when a user reports a conflict, regression, or restored worktree.

## Establish the current boundary

Inspect, in this order as applicable:

1. `git status` and the target-file diff;
2. the target route, parent layout, and direct callers;
3. the current template/script/style sections around the edit;
4. shared components, utilities, and API methods used by that path;
5. the repository's own check commands and encoding conventions.

Separate existing user or colleague changes from changes made for the current request. Do not revert, format, rename, or clean unrelated files. If a stash or save conflict is mentioned, inspect the restored checkout again instead of reconstructing an older version from memory.

## Choose a bounded edit

Before writing, record a small change map:

```text
File and semantic anchor:
Current behavior to preserve:
Confirmed behavior to add or change:
Minimal operation: insert / replace / delete / rename:
New orphaned imports, state, or helpers to remove:
Focused verification:
```

Prefer an anchored patch over a whole-file replacement. Do not use broad search-and-replace for labels, field names, selectors, or API paths when the same text may have different meanings. A rename is safe only after tracing its callers, route names, persistence keys, and tests.

Keep a change local when the requirement is local. A shared refactor is justified only when the ownership, behavior, and contract are genuinely shared and the resulting diff is easier to review than the duplicated code.

## Encoding and conflict discipline

- Read and write source files as UTF-8, preserving the project's newline style where possible.
- Prefer a patch tool or an editor operation scoped to the exact block; do not rewrite a large file through a shell pipeline merely to change a few lines.
- After every bounded patch, inspect the diff and scan changed Chinese text, imports, and delimiters before continuing.
- If a conflict or malformed output appears, stop feature work, identify the last safe state, and repair only the affected block.
- Never use destructive reset/checkout operations to hide uncertainty. Ask before discarding user data or broad changes.

## Review the resulting diff

Every changed line should trace to the requested behavior or to an orphan created by that behavior. Check:

- no accidental text or encoding changes;
- no duplicate methods, keys, imports, or registrations;
- no dead branch left by a removed feature;
- no route or public component contract changed unintentionally;
- no unrelated file was reformatted or overwritten.

Report unrelated pre-existing lint errors separately instead of silently fixing them in the same patch.
