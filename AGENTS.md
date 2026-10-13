# Repository Guidelines

## Read Before Working

Read [README.md](README.md), the relevant issue in the [Loki Linear project](https://linear.app/le-gran-orchestra/project/loki-7bd42d332379), and any documentation added by prior work. The README currently defines prototype scope, proposed boundaries and verification expectations.

## Scope and Decisions

Keep Loki separate from Spry. Focus first on one persistent lightning pickup and a two-player laptop simulation. Distinguish approved requirements from proposals. Do not silently choose a glasses platform or claim that geographic persistence provides world-locked AR. Verify actual Meta APIs and simulator limitations before integrating them.

Record architectural choices, prototype gameplay parameters, sources and limitations when established. Ask for consequential missing product choices; resolve routine implementation details within the authorized issue.

## Implementation and Verification

No framework or dependency tooling is configured yet. Establish reproducible install, development, build, lint, typecheck and test commands with the initial implementation. Use a lockfile and document the supported runtime.

Own verification for each issue. Test persistence across restart, concurrent collection, idempotency, range and ability checks, disconnect recovery, and two-client synchronization as applicable. Report actual commands and results; never claim unrun tests passed or simulated behavior proves hardware support.

## Data and Handoff

Use synthetic coordinates and test identities. Do not commit home addresses, live player locations, credentials or tokens. Keep simulated and physical positioning visibly distinct.

Use concise imperative commit subjects. Pull requests should explain behavior, scope, verification evidence and remaining decisions. Update relevant documentation and Linear status based on evidence, and avoid starting unrelated issues.
