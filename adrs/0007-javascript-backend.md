+++
id = "ADR-0007"
title = "JavaScript Backend"
status = "open"
priority = "medium"
+++

---
title: JavaScript Backend
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed
---


# JavaScript Backend

## Decision

1. **Architecture.** .hnl source │ ▼ Kit (lex + parse)          ← data-driven, same as always │ ▼ AST (handl-platform AstNode) │ ▼ handl-target-js             ← new crate, walks AST → emits JS │ ▼ JavaScript source code │ ▼ Node.js / Browser / Edge
2. **Compilation strategy.**
3. **Arrow combinators as JS functions.** The handl standard library combinators compile to plain JS functions:
4. **Loop compilation.** Handl's `loop` is the most complex construct. It compiles to a JavaScript `while` loop with a state object:
5. **Pattern matching.** Handl's `match` compiles to a JS function with type checks:
6. **Runtime prelude.** The compiled JS includes a small prelude (~100 lines) containing:
7. **Output format.** handl compile --target js arrows/fn/map.hnl -o map.js
8. **Source maps.** The backend emits source map comments linking JS output back to `.hnl` source. This enables:
9. **Integration with existing infrastructure.** The JS backend is a new `handl-target-js` crate that:
10. **What about refinement types?.** The JS backend **does not encode refinement types at runtime**. Refinement types are a compile-time analysis — they guarantee correctness but don't change runtime behavior. The compiled JS is untyped (or optionally typed with JSDoc comments for TypeScript checking).

## Why

Handl programs currently run only via the Rust tree-walking evaluator (`handl-plugin-engine-exec-tree-walk`). This limits handl to environments where a Rust binary can run. There is no way to:

## Not doing

- WASM is harder to debug (no source maps, no readable output).
- WASM can't directly manipulate the DOM or call JS APIs.
- JS is more portable (runs in more environments than WASM).
- A WASM backend can be added later by compiling the Rust evaluator to WASM (different approach, same result).
- TypeScript adds type system complexity that doesn't map cleanly to handl's refinement types.
- TypeScript can't be run directly in browsers or edge workers (requires compilation).

## Consequences

- **Run handl anywhere JS runs** — browsers, Node.js, edge workers, Deno, Bun
- **Web playground** — compile handl to JS in the browser, no server needed
- **npm packages** — distribute handl programs as JS bundles
- **Readable output** — developers can inspect and debug the generated JS
- **Source maps** — stack traces and debugging point back to `.hnl` source

## Enforcement

- Code and tests are named in the design doc.

## Design

The full record (mechanism, tables, proofs, trade-offs): [`design/0007-javascript-backend.md`](../design/0007-javascript-backend.md).
