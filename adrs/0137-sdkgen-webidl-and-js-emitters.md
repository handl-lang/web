---
title: '`sdkgen-webidl` backend and the JS emitters'
type: adr
date: 2026-10-28
status: accepted
status_note: Accepted — extracted in ADR-0128 Phase 5.
---

# ADR-0137: `sdkgen-webidl` backend and the JS emitters

## Context

[ADR-0113](../0113-handl-sdkgen-webidl-js.md) and
[ADR-0115](../0115-handl-sdkgen-dts-js.md) add WebIDL/JS and TypeScript
declaration emission on top of the SDK-generator port
([ADR-0107](../0107-handl-sdk-generator.md));
[ADR-0121](../0121-webidl-cross-spec-includes.md) handles supplementary mixin
specs. These are web-platform concerns, not platform machinery.

## Decision

`web` owns the WebIDL backend and the JS-family emitters:
`plugin-sdkgen-backend-webidl` (target `webidl`) and the JS/`.d.ts` emitter
layer, together with the 13 `generated/*-webidl-browser/` output trees and the
`.webidl`/`.idl` spec inputs.

## Consequences

- The `webidl` target name is preserved (the CLI keeps `hnl sdkgen webidl`);
  the repo is `web`, the module is `sdkgen-webidl` — repo ≠ target.
- `webidl` consumes the `c` backend the same way `python` does, so a WebIDL
  flow is backend `c` + emitter `webidl` unless a pure-IDL backend is added.
- Spec inputs stay gitignored; generated output is committed.
