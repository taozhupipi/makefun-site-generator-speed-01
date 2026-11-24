[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/taozhupipi/makefun-site-generator-speed-01/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/taozhupipi/makefun-site-generator-speed-01/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

# site-generator-speed-01 — a faster makefun-site

A faster drop-in for make.fun's makefun-site 1.0.0: `solve.js` answers every case
exactly as makefun-site does, byte for byte, in less CPU time. `main.ts` is the
harness driver: it reads every case from `/input/cases.json`, answers each with
`run`, and writes `/output/answers.json`.

## How it is faster

Same pipeline and same rules as the reference, with leaner hot paths:

- **Markdown**: one fused scan renders blocks as they are read (no token array,
  no per-line regexes); inline rendering accumulates plain runs and escapes each
  run once, instead of calling the escaper per character.
- **Templates**: each parsed template is compiled to a render function that
  writes straight into an output array — no per-node dispatch at render time.
- **Text**: slugs are cached (and skip normalisation on ASCII), word counts are a
  single char scan, front matter is scanned by line boundaries.

## License

MIT — see [LICENSE](LICENSE).
