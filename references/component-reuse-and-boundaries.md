# Component reuse and boundaries

Use this reference when deciding whether to extract a component, reuse an existing page fragment, or organize new feature files.

## Extract by responsibility

Create or extract a component when it has at least one meaningful boundary:

- independent data ownership or request lifecycle;
- independent interaction and state synchronization;
- stable reuse by multiple consumers;
- a clear semantic business region that benefits from isolated testing or styling.

Do not create a component for every wrapper, one-off visual rectangle, or two blocks that merely look alike. Compare templates, state, events, slots, styles, and ownership before declaring two pieces genuinely reusable.

## Reuse existing UI deliberately

When the user asks to reuse an existing component or page:

1. inspect its actual template, script, styles, props, events, and dependencies;
2. preserve the working structure and visual selectors by default;
3. make only the requested delta;
4. remove only business-specific content that is proven out of scope;
5. verify that loading, empty, error, scroll, footer, and modal behavior were not changed accidentally.

Copying a component and then broadly renaming, restyling, or restructuring it defeats the reuse request. If the copied code carries coupled behavior that the new page does not need, isolate the smallest removable region and state what remains intentionally shared.

## Page, table, filter, and toolbar boundaries

Prefer a small set of stable primitives plus page-owned business composition:

- a generic table may own table chrome, slots, loading/empty presentation, scrolling, and pagination mechanics;
- the page should own columns, query fields, row actions, status semantics, and export/import behavior;
- a filter row should remain page-owned when fields differ materially between screens;
- a shared filter popup is appropriate only when its fields, lifecycle, and visual contract are truly the same;
- a toolbar is best exposed as a slot or composition area, rather than forcing search/import/export into every table.

Split a summary or card at the data and interaction boundary. A reusable metric strip can be separate when its arrangement and semantics are stable; a coupled card containing page-specific filters, date controls, toolbar, and summary should remain one page module until reuse is demonstrated.

## State and routes

Keep state with the owner that can explain its reset and persistence rules. Pass data and events explicitly; avoid hidden module-level mutable state for page interactions.

When adding a page:

- place files under the existing feature directory convention;
- register routes with the repository's established lazy/eager loading pattern;
- preserve existing route paths and public component names unless a migration is intentional;
- trace navigation callers and query parameters before changing them;
- avoid duplicating menu definitions or shells unless the old and new screens have a proven shared owner.

## Styling ownership

Keep component-specific styles close to their component and shared tokens/utilities in the established shared layer. Do not move a large stylesheet merely to make a new component appear cleaner. A selector's ownership, scope, and runtime DOM must remain obvious.
