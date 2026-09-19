# Focused verification and runtime styles

Use this reference after a non-trivial edit, especially for UI, component-library overrides, asynchronous data, or navigation changes.

## Match the check to the risk

Start with the least expensive check that can detect the likely failure:

| Risk | Focused check |
| --- | --- |
| Syntax/import/route registration | parser, type/lint check, or route inspection |
| Changed response mapping | fixture/unit-level inspection or a controlled development request |
| Loading, empty, error, pagination, or stale response | exercise each state in the development environment |
| Navigation/query hydration | inspect the generated URL and destination state after reload |
| CSS override or component-library styling | inspect rendered DOM, compiled selector, winning rule, and computed style |
| Visual layout or interaction | browser check at the relevant viewport, including the affected interaction and crop |

Do not run a full production build by habit. Run it when the user asks, build configuration changed, or a focused check cannot establish a relevant compile risk. A successful build proves compilation only.

## Runtime selector discipline

Before adding a stronger CSS override:

1. inspect the rendered element and actual class/attribute hierarchy;
2. confirm scoped attributes, `:deep`/`::v-deep`, portal/teleport targets, pseudo-elements, and specificity;
3. verify the compiled selector actually matches the DOM;
4. read `getComputedStyle` for the affected geometry, typography, color, border, overflow, transform, and stacking properties;
5. confirm which rule wins.

If the selector misses, correct the DOM ownership or selector first. Do not accumulate `!important` rules as a substitute for diagnosis.

## Layout and component-library defaults

Prefer normal flow, Flex, Grid, and table layout for dynamic content. Use `position: relative` and absolute positioning only for a design-backed overlay or fixed visual anchor. Treat a component library's defaults as behavior to preserve or deliberately override, not as evidence that its visual output matches the design.

For scoped styles, check the framework's actual compiler behavior rather than assuming every deep-selector spelling works. Keep overrides local to the component or feature and avoid changing global defaults for a page-specific defect.

## UI state and visual acceptance

Check that loading is distinguishable from a successful empty result, and that errors do not leave stale rows or an unbounded spinner. Verify hover/focus/active states, scroll behavior, modal/footer ownership, and responsive overflow when they are in scope.

Report visual inspection honestly: a local development render, a computed-style check, and human design acceptance are separate outcomes. Approximate screenshot measurements are estimates unless backed by the design source or a measured runtime value.
