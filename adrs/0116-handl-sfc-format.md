---
title: Handl Single-File Component (`.hfc`) Format
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed.
---


# ADR-0116: Handl Single-File Component (`.hfc`) Format

## Decision

1. **File layout.** An `.hfc` file has three optional regions:
2. **Loader behavior.** 1. Splits the file at region markers (`<script>`, `<template>`, `<style>`). 2. Parses `<script>` and `<script setup>` as a Handl module. 3. Parses `<template>` as a `view` block and runs the `component` transform from ADR-0117. 4. Carries `<style>` as data, rewriting selectors if `scoped` is present and adding the generated scope id to every host element in the `<template>`. 5. Emits a single Handl module plus a CSS string/artifact for the compile-to-JS backend.
3. **`<script>` variants.** available in the template. `state` declarations become reactive state. `props` (when exported as a record) becomes the component's props type. values and arrows are automatically exposed to the template and returned by the setup. This is the default for one-component-per-file files.
4. **Scoped styles.** When `<style scoped>` is present, the loader:
5. **Slots.** Slots are explicit `<slot>` elements. A default slot has no `name`; named slots use `name="..."`. Scoped slots pass data back to the parent through a `let:` attribute on the slot and an `each` attribute for iteration. The lowering is the same Handl callback arrow mechanism described in ADR-0117.

## Why

[ADR-0094 — Generic AST Transform Engine](./0094-generic-ast-transform-engine.md) makes transforms first-class `Ast → Ast` passes. [ADR-0114 — Handl Compile Plugin](./0114-handl-compile-plugin-architecture.md) is planned to lower Handl to JavaScript. [ADR-0115 — `.d.ts` SDKgen](./0115-handl-sdkgen-dts-js.md) will generate Handl port/adapter pairs from NPM package declarations. [ADR-0117 — Handl View / JSX-like Component Syntax](./0117-handl-view-component-syntax.md) defines the inline `view` syntax itself. The missing piece is a file format that bundles the view, the script, and the style into one source file, the way Vue SFCs do.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- One file per component, matching Vue/Astro/Svelte conventions.
- The loader is a small pre-processor; the real syntax work is in ADR-0117.
- The style step is not typechecked by Handl; it is emitted as data for the JS
- Astro/Svelte/Vue/React can share the same `<template>` syntax and just need a

## Enforcement

- Code and tests are named in the design doc.

## Design

The full record (mechanism, tables, proofs, trade-offs): [`design/0116-handl-sfc-format.md`](../design/0116-handl-sfc-format.md).
