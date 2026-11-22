[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/Kuyukbot1/site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/Kuyukbot1/site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

# Site Generator Speed — 22 November 2026

Entry for the [make.fun bounty](https://make.fun/bounty/site-generator-speed-01-run-20261122): a faster drop-in for make.fun's own makefun-site 1.0.0 static site generator, in `solve.js` (Node 22, stdlib only, dependency-free). `run(input)` returns makefun-site 1.0.0's exact answer for every case — the output tree byte for byte — and `main.ts` answers every case in `/input/cases.json` into `/output/answers.json`.

Practice set: **3/3 cases identical** to makefun-site 1.0.0. Speed on the practice set (user CPU, 5 runs of the 3-case set): **~1.35 s vs ~3.1 s for the house baseline — about 2.3× faster**. Also verified on 3 freshly drawn generator sets (9/9 identical, 2.6–2.9× faster) and 1,100 differential-fuzzed random sites (0 mismatches). Two runs produce byte-identical output.
