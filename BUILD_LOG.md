# BUILD_LOG — site-generator-speed-01-run-20261122

## Bounty
- "Build a fast static-site generator" — make.fun bounty site-generator-speed-01-run-20261122
- $100 pot, 10 places x $10, no entry fee, escrowed $100 USDC on-chain (escrow at_open per competition.yaml)
- Entries close 2026-11-24T20:00:00Z (Tue 2026-11-25 03:00 WIB)

## Entry
- `solve.js` (35,761 B) — dependency-free ES module; `run(input)` returns makefun-site 1.0.0's exact output tree. Node 22 stdlib only, no WASM/native code, deterministic, nothing cached between cases.
- `main.ts` (1,441 B) — reads `/input/cases.json` (or `$MAKEFUN_INPUT_DIR`), answers each case with `run`, writes `/output/answers.json` (or `$MAKEFUN_OUTPUT_DIR`); `mkdirSync` only, never deletes the output dir. Sets `--no-incremental-marking` before importing solve.js (the house baseline runs with that flag, and entries may tune V8 flags too).
- Built in 2 genuine passes: a faithful port, then a real speed revision.

## Verification (main agent re-ran the exact submit-repo copies)
- Practice set (`node verify.mjs <kit> ./submit-repo 3`): **3/3 cases identical** to makefun-site 1.0.0 (byte-for-byte vs `practice/reference/expected.json`).
- Speed on practice set (this machine): mine median 222.2 ms vs house baseline 454.4 ms — **2.05x faster**. Build agent's 5-run measurement on the full set: ~1,350 ms vs ~3,100 ms, ~2.3x faster.
- Fresh generator-drawn sets (kit's own `draw.ts`, 3 fake seeds): **9/9 cases identical**, 2.6–2.9x faster.
- Differential fuzz vs the vendor baseline: **1,100 random nasty sites, 0 mismatches**.
- Determinism: `main.ts` end-to-end over the practice set run twice → byte-identical `answers.json` (sha256 25980928b145f54712027939364a64c277098bc4528a2d524e0bc27a0275fb03), 3/3 match expected.
- Docker is not available on this machine, so the kit's `grade-local` reproduce could not be run; verification rests on the local harness above.

## Notes
- The kit ships no `starter/` directory (unlike the tiny-stack-vm kit). The repo LICENSE is the kit vendor makefun-site MIT LICENSE, with the `SPDX-License-Identifier: MIT` line prepended — the kit's license check requires that line (license text alone does not count).
- Sizes: solve.js 35,761 B; main.ts 1,441 B; README.md 1,368 B; LICENSE 1,095 B; BUILD_LOG.md 2,465 B; .makefun/owner.json 56 B. Total 42,186 B — well under the 4 MiB cap.

## Repo
- https://github.com/Kuyukbot1/site-generator-speed-01-run-20261122
