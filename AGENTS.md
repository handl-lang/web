# web

The **web target** — WebIDL/JS SDK emitters, `.hfc` single-file
components, and the JavaScript compile target (ADR-0143; generator
port ADR-0107, WebIDL backend ADR-0113).

## What this repo owns (planned — ADR-0128 Phase 5)

| what | where |
|---|---|
| `plugin-sdkgen-backend-webidl` + the JS emitters (`dts`, `js`) | `modules/sdkgen-webidl` |
| the `.hfc` single-file format and the view-component surface | ADRs 0116, 0117 |
| `plugin-compile-js` — the JavaScript compile target | `modules/compile-js` (ADR-0143) |
| the frontend dialect — custom `.handl` syntax, HMR, dev server | ADRs 0003, 0007, 0021, 0025 |

## Contract

- `host` keeps the compile port and registry
  (`Compiler`/`CompilerRegistry`) and the sdkgen port (`SdkgenTarget` +
  IR). This repo owns the web-specific lowering, the emitters, and the
  generated `*-webidl-browser/` package blocks.
- Status: initialized from the org `project` tree; module extraction
  has not started — WebIDL/JS still builds from
  [`sdkgen-webidl`](https://github.com/handl-lang/sdkgen-webidl), and
  the JS target from [`compile-js`](https://github.com/handl-lang/compile-js).

## Verification

No build yet — nothing is extracted. When `modules/*` lands it follows
the engine-* shape: `workflows/gate.yaml` as the gate (fmt → clippy → test → doc) and
a committed `bupha.toml`.

<!-- myco:agent-awareness -->

## Agent awareness

- Session start / any work discussion: run `myco status --prompt`
  before proposing next steps — know the board first.
- User describes new work → offer to capture it (`myco todo add`,
  `issue new`, `proposal new`). Don't wait to be asked.
- Picking up a task: `myco resume <ID>` is the briefing.
- Wrapping up: `myco handoff <ID>` anything resumable; keep statuses
  honest (claimed → in-progress → blocked/done).

<!-- /myco:agent-awareness -->
