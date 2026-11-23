# sitegen-fast — a faster drop-in for makefun-site 1.0.0

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/c/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/irwan11795/makefun-site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/c/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/irwan11795/makefun-site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/c/site-generator-speed-01-run-20261122)

A faster implementation of makefun-site 1.0.0 for the
[Site Generator Speed](https://make.fun/c/site-generator-speed-01-run-20261122)
competition. `run(input)` returns makefun-site's answer byte for byte on every
case, faster: a fused single-pass Markdown renderer, a template interpreter
that renders each case-constant template once per case, a memoised slugifier,
and manual scanning in place of the reference's per-character escapes.

Pure JavaScript, standard library only. No imports, no network, no clock, no
environment, no randomness. Each case is answered alone: every cache is created
fresh inside `run()` and never carries anything from one case to the next.

## Layout

- `solve.js` — the whole generator: text rules, front matter, Markdown,
  templates, and the build pipeline. Exports `run(input)`.
- `main.ts` — the driver: reads `/input/cases.json`, answers each case with
  `run()`, writes `/output/answers.json`. (Outside a container,
  `MAKEFUN_INPUT_DIR` and `MAKEFUN_OUTPUT_DIR` stand in for `/input` and
  `/output`.)
- `package.json` — `{"type": "module"}`, so the entry loads as an ES module.

## Local check

On the kit's practice set (3 cases) the entry's answers match the kit's
`expected.json` byte for byte, and its `run()` measures about a third of the
house baseline's time on this machine.
