---
title: '`compile-js` target'
type: adr
date: 2026-10-28
status: accepted
status_note: Accepted — extracted in ADR-0128 Phase 5.
---

# ADR-0143: `compile-js` target

## Context

[ADR-0114](../0114-handl-compile-plugin-architecture.md) states the compile
port (`Compiler` / `CompilerRegistry`); `plugin-ext-compile`'s dispatcher
statically registers every compiler, and `host-cli` statically depends on
`plugin-compile-js`. JS emission is a web concern.

## Decision

`web` owns the JS compiler: `plugin-compile-js` (target `js`), including its
lowering (and the `proof.rs` `Path`/`Equiv` lowerers — currently implemented
but never dispatched), together with the JS/`.hfc`/view surfaces of
[ADR-0116](../0116-handl-sfc-format.md) and
[ADR-0117](../0117-handl-view-component-syntax.md).

`host` keeps the port and the registry seam; a host opts the target in via
a feature on its own manifest.

## Consequences

- `host-cli`'s dependency on `plugin-compile-js` becomes an explicit git dep
  in `cli/` — the `hnl` binary's target set *is* its dep list.
- The static `registry.register(Box::new(JsCompiler))` in the platform
  dispatcher is deleted; the target is registered from this module.
- A JS-specific change no longer rebuilds the platform workspace.
