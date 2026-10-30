---
title: Handl View / JSX-like Component Syntax for JS Targets
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed.
---


# ADR-0117: Handl View / JSX-like Component Syntax for JS Targets

## Decision

1. **Syntax.** A `view` is a named arrow that returns a JS value:
2. **Lowering rules.** Vue target). resolves to a Handl arrow.
3. **Slots.** Slots are explicit `<slot>` elements:
4. **Reactive state.** A `state` block declares component-local reactive state:
5. **Target binding.** The transform is target-agnostic. A compile-time `target` config picks the runtime calls:

## Why

[ADR-0115 — `.d.ts` SDKgen](./0115-handl-sdkgen-dts-js.md) will make JS frameworks reachable as low-level Handl arrows (`createElement`, `h`, `useState`, `ref`). That is verbose. [ADR-0116 — `.hfc` SFC Format](./0116-handl-sfc-format.md) packages the view into a file with `<template>`, `<script>`, and `<style>`. This ADR defines the inline view syntax itself.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- The `component` pass is a pure `Ast → Ast` transform and can be previewed,
- SFC packaging is handled separately in ADR-0116.
- The syntax is small and not framework-specific; adding Astro, Svelte, or Solid
- Out of scope for the first version: framework-specific lifecycle hooks

## Enforcement

- Code and tests are named in the design doc.

## Design

The full record (mechanism, tables, proofs, trade-offs): [`design/0117-handl-view-component-syntax.md`](../design/0117-handl-view-component-syntax.md).
