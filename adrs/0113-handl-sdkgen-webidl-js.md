---
title: Handl SDK Generator — WebIDL / JS Backend
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed.
---


# ADR-0113: Handl SDK Generator — WebIDL / JS Backend

## Decision


Add a `plugin-sdkgen-backend-webidl` crate that parses WebIDL files and produces
`SdkgenModule` records.

- The backend consumes one or more `.webidl` files (e.g. the W3C specs).
- The `client_package` for the generated adapter is `js`.
- The adapter uses `js.call` / `js.errno()` primitives (a new `js` client
  package) to invoke foreign JS functions at runtime.
- Map common WebIDL types to Handl types:
  - `long` / `long long` → `Int` (`i32` / `i64`)
  - `double` / `float` → `Float` (`f64` / `f32`)
  - `DOMString` / `USVString` → `String` (`js_string`)
  - `ArrayBufferView` / `BufferSource` → `Bytes` (`js_bytes`)
  - `object` / `any` / interface references → `Handle` (`js_object`)
  - `void` → `()`
- Support `interface`, `dictionary`, `enum`, `callback function`, and
  `namespace` (static methods).
- The first target runtime is **Deno / Browser** because both expose standard
  Web APIs without an extra native binding step. Node support can follow later.


## Why

[ADR-0107 — Handl SDK Generator](./0107-handl-sdk-generator.md) established a backend-agnostic `SdkgenModule` IR and a port-adapter emitter. The C backend (`plugin-sdkgen-backend-c`) is the first concrete implementation. The next high-priority target is the Web platform: Handl running in browsers, Deno, or Node must be able to call existing Web APIs (WebGL, WebGPU, DOM, etc.) and first-class `.webidl` definitions.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- Handl can consume the Web platform API surface directly.
- A `js` client package must be designed and implemented, paralleling `ffi` and
- WebIDL overloads and optional arguments require a name-mangling / defaulting
- This backend is, by request, the highest-priority future backend in the SDK

## Enforcement

- `plugin-sdkgen-backend-webidl` — where this is true.
- `plugin-sdkgen-backend-c` — where this is true.

## Design

The full record (context, tables, phases, trade-offs): [`design/0113-handl-sdkgen-webidl-js.md`](../design/0113-handl-sdkgen-webidl-js.md).
