---
title: Decisions
type: index
---

# Decisions

One line per decision rule, generated from each ADR's `## Decision`
section with `host/scripts/gen-decisions.py`. The ADR is the argument;
this is the recall surface (ADR-0161 §8). Superseded records are excluded.

### handl Frontend: Custom `.handl` Syntax

- **Syntax.** // Line comment user => http.get("https://api.example.com/users/1") — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **How the parser distinguishes fields from data.** No fields: section is needed. The syntax form is the discriminator: — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Output mapping.** — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Type inference rules.** The frontend omits type: when the type is obvious: — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Implementation plan.** 1. **New crate handl-frontend-handl** — implements Frontend trait. 2. **Parser** —… — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Verbosity comparison.** YAML remains slightly more compact for pure data objects. .handl wins everywhere else,… — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)

### JavaScript Backend

- **Architecture.** .hnl source │ ▼ Kit (lex + parse) ← data-driven, same as always │ ▼ AST (handl-platform AstNode) │ ▼… — [ADR-0007](adrs/0007-javascript-backend.md)
- **Compilation strategy.** — [ADR-0007](adrs/0007-javascript-backend.md)
- **Arrow combinators as JS functions.** The handl standard library combinators compile to plain JS functions: — [ADR-0007](adrs/0007-javascript-backend.md)
- **Loop compilation.** Handl's loop is the most complex construct. It compiles to a JavaScript while loop with a state… — [ADR-0007](adrs/0007-javascript-backend.md)
- **Pattern matching.** Handl's match compiles to a JS function with type checks: — [ADR-0007](adrs/0007-javascript-backend.md)
- **Runtime prelude.** The compiled JS includes a small prelude (~100 lines) containing: — [ADR-0007](adrs/0007-javascript-backend.md)
- **Output format.** handl compile --target js arrows/fn/map.hnl -o map.js — [ADR-0007](adrs/0007-javascript-backend.md)
- **Source maps.** The backend emits source map comments linking JS output back to .hnl source. This enables: — [ADR-0007](adrs/0007-javascript-backend.md)
- **Integration with existing infrastructure.** The JS backend is a new handl-target-js crate that: — [ADR-0007](adrs/0007-javascript-backend.md)
- **What about refinement types?.** The JS backend **does not encode refinement types at runtime**. Refinement types are… — [ADR-0007](adrs/0007-javascript-backend.md)

### Hot Module Replacement (HMR)

- **Components.** ┌──────────────┐ file change ┌──────────────┐ │ handl │ ────────────────▶ │ HmrServer │ │ documents │ │… — [ADR-0021](adrs/0021-hmr.md)
- **WebSocket protocol.** Messages are JSON over WebSocket — [ADR-0021](adrs/0021-hmr.md)
- **Document surface.** hmr may appear at the document level and on individual declarations. Declaration-level settings… — [ADR-0021](adrs/0021-hmr.md)
- **Lifecycle.** 1. The dev server detects a file change. 2. It reloads the document, validates it, and computes a diff.… — [ADR-0021](adrs/0021-hmr.md)
- **Host integration.** Hosts can extend HMR by registering custom update handlers. For example, Peregrin's host might… — [ADR-0021](adrs/0021-hmr.md)

### ADR-0025 (Remaining): HTTP Client/Server v1.x and v2 Enhancements

- **handl FunctionValue route handler dispatch.** The abstract route and route_function methods are stubbed with… — [ADR-0025](adrs/0025-http-server-remaining.md)
- **TLS termination.** Add TLS/HTTPS support via rustls or native TLS, with certificate loading and SNI support — [ADR-0025](adrs/0025-http-server-remaining.md)
- **Middleware hooks.** Provide a composable middleware/layer API for request/response interception (similar to tower or… — [ADR-0025](adrs/0025-http-server-remaining.md)
- **Compression.** Add transparent gzip/brotli response compression with Accept-Encoding negotiation — [ADR-0025](adrs/0025-http-server-remaining.md)
- **CORS and rate-limiting.** Provide built-in CORS policy handling and per-IP or per-handler rate-limiting — [ADR-0025](adrs/0025-http-server-remaining.md)

### Handl SDK Generator — WebIDL / JS Backend

- The backend consumes one or more .webidl files (e.g. the W3C specs) — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- The client_package for the generated adapter is js — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- The adapter uses js.call / js.errno() primitives (a new js client — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- Map common WebIDL types to Handl types: — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- long / long long → Int (i32 / i64) — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- double / float → Float (f64 / f32) — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- DOMString / USVString → String (js_string) — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- ArrayBufferView / BufferSource → Bytes (js_bytes) — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- object / any / interface references → Handle (js_object) — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- void → () — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- Support interface, dictionary, enum, callback function, and — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)
- The first target runtime is **Deno / Browser** because both expose standard — [ADR-0113](adrs/0113-handl-sdkgen-webidl-js.md)

### Handl SDK Generator — TypeScript Declaration (.d.ts) Backend

- **Example: using an NPM package from Handl.** A function-oriented package like express ships .d.ts declarations.… — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- **Function libraries vs. component frameworks.** This works well for function/value-oriented packages: Express, Lodash,… — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- **Scope and limitations.** The first version targets the subset of .d.ts that is sufficient for NPM libraries and… — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- **Parser choice.** The backend wraps a .d.ts parser behind the SdkgenBackend trait. The first implementation candidate… — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)

### Handl Single-File Component (`.hfc`) Format

- **File layout.** An .hfc file has three optional regions: — [ADR-0116](adrs/0116-handl-sfc-format.md)
- **Loader behavior.** 1. Splits the file at region markers (<script>, <template>, <style>). 2. Parses <script> and… — [ADR-0116](adrs/0116-handl-sfc-format.md)
- **<script> variants.** available in the template. state declarations become reactive state. props (when exported as a… — [ADR-0116](adrs/0116-handl-sfc-format.md)
- **Scoped styles.** When <style scoped> is present, the loader: — [ADR-0116](adrs/0116-handl-sfc-format.md)
- **Slots.** Slots are explicit <slot> elements. A default slot has no name; named slots use name="...". Scoped slots… — [ADR-0116](adrs/0116-handl-sfc-format.md)

### Handl View / JSX-like Component Syntax for JS Targets

- **Syntax.** A view is a named arrow that returns a JS value: — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- **Lowering rules.** Vue target). resolves to a Handl arrow — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- **Slots.** Slots are explicit <slot> elements: — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- **Reactive state.** A state block declares component-local reactive state: — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- **Target binding.** The transform is target-agnostic. A compile-time target config picks the runtime calls: — [ADR-0117](adrs/0117-handl-view-component-syntax.md)

### WebIDL Cross-Spec `includes` — Supplementary Mixin Specs

- streams.idl — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- WebIdlConfig.includes: Vec<String> — paths relative to the config — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- WebIdlBackend::add_include_spec(path) registers each path; during — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- Diagnostics are preserved: supplementary parse diagnostics are tagged — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- Emission granularity is unchanged: one spec → one package. Encoding — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)

### Step-Arrow Concurrency: Handl-Authored Scheduler over epoll

- **B0 (now)**: handl-packages/concurrent/concurrent.hnl defines the step — [ADR-0122](adrs/0122-step-arrow-concurrency.md)
- **B1 (later)**: a free-algebra interpreter (à la arrow_model.hnl) that — [ADR-0122](adrs/0122-step-arrow-concurrency.md)
