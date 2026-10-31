+++
id = "ADR-0003"
title = "handl Frontend: Custom `.handl` Syntax"
status = "open"
priority = "medium"
+++

---
title: 'handl Frontend: Custom `.handl` Syntax'
type: adr
date: 2026-10-28
status: proposed
status_note: Proposed
---


# handl Frontend: Custom `.handl` Syntax

## Decision

1. **Syntax.** // Line comment user => http.get("https://api.example.com/users/1")
2. **How the parser distinguishes fields from data.** No `fields:` section is needed. The syntax form is the discriminator:
3. **Output mapping.**
4. **Type inference rules.** The frontend omits `type:` when the type is obvious:
5. **Implementation plan.** 1. **New crate `handl-frontend-handl`** — implements `Frontend` trait. 2. **Parser** — hand-written or `pest`/`nom` PEG parser. 3. **Codegen** — walks AST, emits `serde_json::Value` in canonical structure (1:1 mapping, no logic). 4. **Register in `frontend_for`** — add `"handl"` match arm in `handl-frontend/src/lib.rs`. 5. **Source map** — implement `parse_with_locations` for type error reporting (line/column tracking).
6. **Verbosity comparison.** YAML remains slightly more compact for pure data objects. `.handl` wins everywhere else, especially for functions and parameterized fields.

## Why

handl documents are currently written in YAML (or JSON, TOML). The `Frontend` trait (`handl-runtime::Frontend`) abstracts format parsing — each frontend parses text into `NonFunctionValue` and the downstream pipeline (field extraction, type checking, typegen, VM) operates on the value, unaware of the source format.

## Not doing

- none recorded — legacy record; the design doc lists what was deferred.

## Consequences

- 69% line reduction for typical documents.
- Type inference eliminates redundant `type:` declarations.
- Brace-based schemas are visually cleaner than nested YAML maps.
- Arrow syntax unifies fields and functions under one mental model.
- Zero downstream changes — same `NonFunctionValue`, same pipeline.

## Enforcement

- Code and tests are named in the design doc.

## Design

The full record (mechanism, tables, proofs, trade-offs): [`design/0003-ac-frontend-custom-syntax.md`](../design/0003-ac-frontend-custom-syntax.md).
