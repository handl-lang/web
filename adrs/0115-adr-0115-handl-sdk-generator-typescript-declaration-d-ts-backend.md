+++
id = "ADR-0115"
title = "ADR-0115: Handl SDK Generator — TypeScript Declaration (.d.ts) Backend"
status = "open"
priority = "medium"
+++

---
title: Handl SDK Generator — TypeScript Declaration (.d.ts) Backend
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed.
---


# ADR-0115: Handl SDK Generator — TypeScript Declaration (.d.ts) Backend

## Decision

1. **Example: using an NPM package from Handl.** A function-oriented package like `express` ships `.d.ts` declarations. Running `hnl sdkgen dts` over them produces a port and a `js` adapter, and the resulting Handl source looks like any other imported module:
2. **Function libraries vs. component frameworks.** This works well for function/value-oriented packages: Express, Lodash, Axios, `fs`, `crypto`, etc.
3. **Scope and limitations.** The first version targets the subset of `.d.ts` that is sufficient for NPM libraries and server frameworks: modules, namespaces, interfaces, type aliases, function and method declarations, constants, enums, and callback types.
4. **Parser choice.** The backend wraps a `.d.ts` parser behind the `SdkgenBackend` trait. The first implementation candidate is a Rust-based TypeScript parser (e.g. `swc`, `oxc_parser`, or `tree-sitter-typescript`). The parser crate is a private dependency of `plugin-sdkgen-backend-dts`; changing it does not affect the public `SdkgenBackend` API or the emitted Handl source. A parser evaluation and selection step is part of Phase 0.

## Why

[ADR-0107 — Handl SDK Generator](./0107-handl-sdk-generator.md) established a backend-agnostic `SdkgenModule` IR and a port-adapter emitter. The C backend (`plugin-sdkgen-backend-c`) is implemented, and the WebIDL/JS backend ([ADR-0113](./0113-handl-sdkgen-webidl-js.md)) is the next high-priority target for Web platform APIs.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- The large JavaScript ecosystem becomes reachable from Handl without manual
- Component ergonomics (`.hfc` and `view` syntax) are handled separately by
- `.d.ts` is richer and more heterogeneous than WebIDL or C headers; the backend
- Structural typing and advanced TS features do not map one-to-one to Handl's
- The WebIDL and `.d.ts` backends share the same `js` client package and adapter

## Enforcement

- `plugin-sdkgen-backend-dts` — where this is true.
- `plugin-sdkgen-backend-c` — where this is true.

## Design

The full record (mechanism, tables, proofs, trade-offs): [`design/0115-handl-sdkgen-dts-js.md`](../design/0115-handl-sdkgen-dts-js.md).
