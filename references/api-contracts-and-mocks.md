# API contracts and development mocks

Use this reference when adding or changing API methods, page data loading, uploads/downloads, or temporary data.

## Keep API modules thin

An API wrapper should own the HTTP method, endpoint, request location (`params`, `data`, or upload body), and any required transport options. Add a short comment above each non-trivial wrapper describing its business purpose and confirmed filters. Keep page state, display labels, and response shaping in the consuming module.

Do not invent fields, response guarantees, or status mappings because a screen needs them. If a field is missing, classify the gap and either use an explicitly agreed temporary value or stop the integration pending a contract decision.

## Handle responses at the page boundary

Page methods should normally:

- set and clear a local loading state;
- call the wrapper with the current query state;
- read the repository's established response envelope;
- update rows, totals, options, or detail state;
- show a useful error through the existing notification convention;
- preserve an explicit empty result as empty rather than replacing it with mock data.

Keep response handling direct. Add a small adapter only when a transformation is shared, non-trivial, or required at more than one boundary. Avoid a universal normalizer with speculative aliases, repeated type checks, or silent fallback values.

For concurrent or rapidly changing filters, protect state from stale responses with the repository's established request-version, cancellation, or equivalent pattern. Do not add elaborate cancellation machinery to a one-shot request without a demonstrated stale-response risk.

## Record contract certainty

For each integration, classify the contract:

| Classification | Implementation rule |
| --- | --- |
| Documented and structurally sufficient | Integrate directly. |
| Confirmed verbally but documentation lags | Integrate only the confirmed shape and record the documentation gap. |
| Frontend-led proposed shape | Integrate against the explicit proposal and mark it as a pending backend contract. |
| Missing field with an agreed temporary value | Add the smallest local temporary value and mark its removal point. |
| Unknown or structurally incompatible response | Do not pretend it is integrated; list the required shape. |
| Missing endpoint | Keep an explicit mock or disabled path, never a fabricated production call. |
| Retired field or behavior | Remove its active logic once the replacement is confirmed; do not grow a permanent compatibility layer. |

Keep this record close to the task handoff or a project contract note, not embedded as stale business history in a generic utility.

## Mock boundaries

Use a small typed mock only when the real endpoint or contract is unavailable and the user authorizes development-only behavior. The mock should:

- live beside the feature or in the repository's established mock location;
- resemble the intended response shape without hiding contract gaps;
- be enabled by an obvious development-only switch or branch;
- preserve loading, empty, and error states as independently testable states;
- be removed together with its import, switch, and fallback branch after integration.

Never fall back to mock data merely because the real endpoint returned an empty list or a valid zero. Never describe mock rendering as backend or persistence validation.

## File transfer methods

Inspect the actual contract before choosing a transport:

- a file stream needs the repository's blob/response-type handling and a safe filename;
- a returned download URL should be opened or downloaded as a URL, not decoded as a stream;
- an upload needs the existing multipart convention, field name, and visible progress/error behavior.

Keep export filenames user-readable and derive them from the business view, not internal tab keys or implementation enum names.
