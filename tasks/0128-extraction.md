# Task 0128 — `web/` extraction (ADR-0128 Phase 5)

Expand ADR-0128 Phase 5 for this repo. The docs are already on
this `project` branch; the code lands with the extraction.

## Docs owned here

- `adrs/0137-sdkgen-webidl-and-js-emitters.md` — sdkgen-webidl backend and the JS emitters
- `adrs/0143-compile-js-target.md` — compile-js target
- split parent `0107-handl-sdk-generator.md` (canonical half stays in `host`)
- split parent `0114-handl-compile-plugin-architecture.md` (canonical half stays in `host`)

## Extraction

- [x] Follow ADR-0128 Phase 5: create the repo's workspace,
      move the crates/packages named there, wire the git dep + `[patch]`.
      **Done (crates):** `modules/{sdkgen-webidl,compile-js}`
      (subtree-split history, package names unchanged). The `.hnl` web
      package block + `generated/*-webidl-browser/` dirs stay in
      platform pending the ADR-0128 item-7 C-ABI decision — they share
      a relative-import closure with the deferred `-c` packages.
- [x] Keep `main` a clean build tree (`/project/` ignored).
- [x] Flip the split children from `Proposed` to `Accepted` when the
      code actually moves.
