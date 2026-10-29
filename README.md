# web

The **web target** — WebIDL/JS SDK emitters, `.hfc` single-file components, and
the JavaScript compile target (ADR-0143; generator port ADR-0107, WebIDL
backend ADR-0113).

## What this repo owns

| what | where |
|---|---|
| `plugin-sdkgen-backend-webidl` + the JS emitters (`dts`, `js`) | `modules/sdkgen-webidl` (ADR-0128 Phase 5) |
| the `.hfc` single-file format and the view-component surface | ADRs 0116, 0117 |
| `plugin-compile-js` — the JavaScript compile target | `modules/compile-js` (ADR-0143) |
| the frontend dialect — custom `.handl` syntax, HMR, dev server | ADRs 0003, 0007, 0021, 0025 |

`host` keeps the compile port and registry (`Compiler`/`CompilerRegistry`) and
the sdkgen port (`SdkgenTarget` + IR). This repo owns the web-specific
lowering, the emitters, and the generated `*-webidl-browser/` package blocks.

## Status

Initialized from the org `project` tree. The module extractions (ADR-0128
Phases 5) have not started: WebIDL/JS still builds from
[`sdkgen-webidl`](https://github.com/handl-lang/sdkgen-webidl), and the JS
target from [`compile-js`](https://github.com/handl-lang/compile-js).

## Development

No build here yet — nothing is extracted. When `modules/*` lands it follows the
engine-* shape: `ci.sh` as the gate (fmt → clippy → test → doc) and a committed
`bupha.toml`.

## Documentation

Published site (Diátaxis): <https://handl-lang.github.io/docs/web/>

Decision records live on the `project` branch under `project/adrs/`; the
layout rule is ADR-0162 (`host` repo, `project` branch).

## License

MIT.
