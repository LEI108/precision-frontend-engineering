# Comments and copyable handoffs

Use this reference when writing or reviewing code comments, or when the requested deliverable is a precise modification block rather than a direct edit.

## Comment quality gate

Comments should help the next developer understand what a region is, what important code is responsible for, or why a non-obvious decision exists. Keep most comments to one or two lines and update or remove them when behavior changes.

Comment these when they are not obvious from the code:

- major business or interaction regions in a template;
- state or constants with special lifetime, unit, source, reset, or coupling rules;
- important API wrappers and business/data-adapter methods;
- stale-response protection, state synchronization, and meaningful transformations;
- compatibility workarounds, derived styles, browser limitations, and deliberate deviations;
- chart options whose series order or encoding has business meaning.

Avoid comments that merely narrate syntax, such as “loop through items” above a `map`, or vague labels such as “special handling” and “prevent errors”. Do not preserve comments that describe retired behavior as if it were still active.

## Precise modification blocks

When the user asks for copyable changes, do not replace a whole component unless the file is genuinely new or the user explicitly requests a rewrite. Identify the file and a semantic anchor rather than relying on a line number that will drift.

Use this shape:

```text
文件：<path>
定位锚点：<method / selector / template block / import>
当前代码特征：<short unique description>
操作：新增 / 局部替换 / 删除 / 重命名

<copyable code block>

保留内容：<what must stay unchanged>
原因：<confirmed behavior or contract>
影响范围：<callers, route, state, or style boundary>
验证：<smallest check and its boundary>
```

For several edits, order blocks by dependency and split them into reviewable steps. Call out any user-owned or pre-existing code that the block intentionally does not touch.

## Handoff language

Separate these statements:

- changed in the worktree;
- statically checked;
- rendered in a development server;
- exercised with a real backend;
- inspected in a browser at the target viewport;
- visually accepted by a human.

If a check was not run, say so. If a value is derived from design evidence or an assumption, label it instead of presenting it as source truth.
