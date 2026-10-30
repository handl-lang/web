---
title: Decisions
type: index
---

# Decisions

One line per decision rule, generated from each ADR's `## Decision`
section with `host/scripts/gen-decisions.py`. The ADR is the argument;
this is the recall surface (ADR-0161 §8). Superseded records are excluded.

### handl Frontend: Custom `.handl` Syntax

- x |> f(args...) → f(args..., x) — pipe inserts value as last argument — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- x |> f(a) |> g(b) → g(b, f(a, x)) — chains nest inside-out — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- f >> g >> h → fp.flow(f, g, h) — returns a function — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- f << g << h → fp.compose(f, g, h) — returns a function — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- |> is **zero-cost** — pure frontend desugaring to nested calls, no — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- >> and << require fp.flow and fp.compose to be added to — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- a ?? b → fp.default(a, b) — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- a ?? b ?? c → fp.coalesce(a, b, c) — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- a?.path → fp.default(a, {}).path (access on empty object returns null) — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- a?.b?.c → fp.default(fp.default(a, {}).b, {}).c — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- inherit — value flows down to nested scopes during scoped — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- lock — value cannot be overridden in nested scopes — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- spread — field's object value is spread into parent, field — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **New crate handl-frontend-handl** — implements Frontend trait — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Parser** — hand-written or pest/nom PEG parser — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Codegen** — walks AST, emits serde_json::Value in canonical — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Register in frontend_for** — add "handl" match arm in — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)
- **Source map** — implement parse_with_locations for type error — [ADR-0003](adrs/0003-ac-frontend-custom-syntax.md)

### JavaScript Backend

- comp, first, choice, loop, doBlock, returnA — combinator implementations — [ADR-0007](adrs/0007-javascript-backend.md)
- match, matchPattern — pattern matching helpers — [ADR-0007](adrs/0007-javascript-backend.md)
- arr — stdlib lookup — [ADR-0007](adrs/0007-javascript-backend.md)
- Spread/rest helpers for array destructuring — [ADR-0007](adrs/0007-javascript-backend.md)
- Stack traces pointing to .hnl lines — [ADR-0007](adrs/0007-javascript-backend.md)
- Debugger breakpoints in .hnl source (with source map support) — [ADR-0007](adrs/0007-javascript-backend.md)
- Implements Plugin from handl-platform — [ADR-0007](adrs/0007-javascript-backend.md)
- Contributes a Behavior<Target> for the Target operation — [ADR-0007](adrs/0007-javascript-backend.md)
- Walks AstNode trees and emits JS strings — [ADR-0007](adrs/0007-javascript-backend.md)
- Uses the same Kit for parsing (no separate parser) — [ADR-0007](adrs/0007-javascript-backend.md)
- @param {number[]} input — [ADR-0007](adrs/0007-javascript-backend.md)
- @returns {number[]} — [ADR-0007](adrs/0007-javascript-backend.md)
- @refinement Sorted(input) → Sorted(output) — [ADR-0007](adrs/0007-javascript-backend.md)

### Hot Module Replacement (HMR)

- **HmrServer** (dev server). Watches document files and any import() — [ADR-0021](adrs/0021-hmr.md)
- **HmrClient** (runtime). Receives WebSocket messages inside the running — [ADR-0021](adrs/0021-hmr.md)
- **HmrUpdateHandler**. Applies the diff to the running module. It retires — [ADR-0021](adrs/0021-hmr.md)
- **HmrUpdate schema**. A typed JSON message describing the delta. It is — [ADR-0021](adrs/0021-hmr.md)
- { "type": "hmr:ready" } — [ADR-0021](adrs/0021-hmr.md)
- { "type": "hmr:custom", "payload": ... } — [ADR-0021](adrs/0021-hmr.md)
- { "type": "hmr:update", "added": [...], "removed": [...], "changed": [...] } — [ADR-0021](adrs/0021-hmr.md)
- { "type": "hmr:full-reload", "reason": "..." } — [ADR-0021](adrs/0021-hmr.md)
- { "type": "hmr:error", "error": "..." } — [ADR-0021](adrs/0021-hmr.md)
- accept (boolean or list of names). Whether the changed declaration can — [ADR-0021](adrs/0021-hmr.md)
- decline (list of names). Declarations that always force full-reload — [ADR-0021](adrs/0021-hmr.md)
- before / after. Expressions to evaluate before and after the HMR delta — [ADR-0021](adrs/0021-hmr.md)
- dispose. Expression to evaluate before an old declaration is removed or — [ADR-0021](adrs/0021-hmr.md)
- prune. Expression to evaluate after a declaration is removed — [ADR-0021](adrs/0021-hmr.md)
- data. A map of values to carry across updates for the same declaration — [ADR-0021](adrs/0021-hmr.md)
- invalidate. A list of downstream declarations that must also be reloaded — [ADR-0021](adrs/0021-hmr.md)
- on_error (document-level only). One of full-reload, cancel, or — [ADR-0021](adrs/0021-hmr.md)
- The dev server detects a file change — [ADR-0021](adrs/0021-hmr.md)
- It reloads the document, validates it, and computes a diff — [ADR-0021](adrs/0021-hmr.md)
- If any changed or removed declaration is not accepted for HMR, the server — [ADR-0021](adrs/0021-hmr.md)
- For an accepted delta: — [ADR-0021](adrs/0021-hmr.md)
- Evaluate before expressions — [ADR-0021](adrs/0021-hmr.md)
- For removed declarations, evaluate dispose and prune, then remove — [ADR-0021](adrs/0021-hmr.md)
- For changed declarations, evaluate dispose, remove the old definition, — [ADR-0021](adrs/0021-hmr.md)
- For new declarations, inject them — [ADR-0021](adrs/0021-hmr.md)
- Evaluate after expressions — [ADR-0021](adrs/0021-hmr.md)

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

- The backend consumes one or more .d.ts files (e.g. from an NPM package's — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- The client_package for the generated adapter is js, reusing the primitives — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- The backend maps .d.ts concepts to Handl types and arrows: — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- The output layout follows the established pattern from ADR-0107: — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- **Port** — abstract export arrows and types, platform-agnostic — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- **Adapter** — concrete export ... := arrows that call js.call and — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- d.ts overloads and optional arguments use the same name-mangling / defaulting — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- A per-package .sdkgen.yaml provides overrides for information that cannot be — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- default vs. named exports, — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- mutable classes and stateful methods, — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- custom marshalling for unusual types, — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- side-effecting module imports, — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- whether a function throws (maps to Result<_, JsError>) or returns a raw — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- Generics other than monomorphization of a few common instantiations — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- Conditional, mapped, template-literal, and recursive conditional types — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- JSX/component view syntax and .hfc packaging — these are not part of — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- Class inheritance, abstract classes, and protected/private members — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)
- Module augmentation and ambient module declarations — [ADR-0115](adrs/0115-handl-sdkgen-dts-js.md)

### Handl Single-File Component (`.hfc`) Format

- Splits the file at region markers (<script>, <template>, <style>) — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Parses <script> and <script setup> as a Handl module — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Parses <template> as a view block and runs the component transform from — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Carries <style> as data, rewriting selectors if scoped is present and — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Emits a single Handl module plus a CSS string/artifact for the compile-to-JS — [ADR-0116](adrs/0116-handl-sfc-format.md)
- <script>: ordinary module. exported names are the public API and are — [ADR-0116](adrs/0116-handl-sfc-format.md)
- <script setup> (Vue-style): the entire region is a setup function. Top-level — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Generates a unique scope id for the file — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Rewrites CSS selectors to include the scope attribute — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Adds the scope id to every host element in the <template> — [ADR-0116](adrs/0116-handl-sfc-format.md)
- Emits the processed CSS as a string that the compile-to-JS backend writes to a — [ADR-0116](adrs/0116-handl-sfc-format.md)

### Handl View / JSX-like Component Syntax for JS Targets

- <tag> is sugar for createElement("tag", attrs, children) (or h for the — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- <Tag ...> is a component call; the tag must be a capitalized identifier that — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- attr="val" becomes #{ attr: "val" } — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- attr={expr} becomes #{ attr: expr } — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- {expr} inside a tag is text interpolation or a child expression — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- v-if="cond" / v-else become ordinary if/else — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- @event="handler" becomes an event attribute such as #{ onClick: handler } — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- Capitalized tags are components; lowercase tags are host elements — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- A view is just a named arrow, so it composes with ordinary Handl code — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- A default slot has no name — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- Named slots use name="..." — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- Scoped slots use let: to name the data passed back and each: to iterate a — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- target = "react" → createElement, useState, etc — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- target = "vue" → h, ref, reactive, render_slot, etc — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- target = "svelte" → Svelte runtime calls or .svelte source output — [ADR-0117](adrs/0117-handl-view-component-syntax.md)
- target = "dom" → document.createElement, document.body.append — [ADR-0117](adrs/0117-handl-view-component-syntax.md)

### WebIDL Cross-Spec `includes` — Supplementary Mixin Specs

- streams.idl — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- WebIdlConfig.includes: Vec<String> — paths relative to the config — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- WebIdlBackend::add_include_spec(path) registers each path; during — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- Diagnostics are preserved: supplementary parse diagnostics are tagged — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)
- Emission granularity is unchanged: one spec → one package. Encoding — [ADR-0121](adrs/0121-webidl-cross-spec-includes.md)

### Step-Arrow Concurrency: Handl-Authored Scheduler over epoll

- **B0 (now)**: handl-packages/concurrent/concurrent.hnl defines the step — [ADR-0122](adrs/0122-step-arrow-concurrency.md)
- **B1 (later)**: a free-algebra interpreter (à la arrow_model.hnl) that — [ADR-0122](adrs/0122-step-arrow-concurrency.md)
