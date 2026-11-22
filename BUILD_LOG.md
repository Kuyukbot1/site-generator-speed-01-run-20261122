# BUILD_LOG — site-generator-speed-01-run-20261122

## Bounty
- "Build a fast static-site generator" — make.fun bounty site-generator-speed-01-run-20261122
- $100 pot, 10 places x $10, no entry fee, escrowed $100 USDC (escrow at_open per competition.yaml)
- Entries close 2026-11-24T20:00:00Z (Tue 2026-11-25 03:00 WIB)

## Entry
- `solve.js` (35,761 B, sha256 93b47d927ece3ab0b0afdf13b407fcf08062b2bd228f39745a89534a45366686) — dependency-free ES module; `run(input)` returns makefun-site 1.0.0's exact output tree. Node 22 stdlib only, no WASM/native code, deterministic, nothing cached between cases.
- `main.ts` (1,441 B, sha256 e15d5871b58bceca37cd176aa25a2069017139de4dab40871caa9a06a513e131) — reads `/input/cases.json` (or `$MAKEFUN_INPUT_DIR`), answers each case with `run`, writes `/output/answers.json` (or `$MAKEFUN_OUTPUT_DIR`); `mkdirSync` only, never deletes the output dir. Sets `--no-incremental-marking` before importing solve.js (the house baseline runs with that flag, and entries may tune V8 flags too).
- Built in 2 genuine passes: a faithful port, then a real speed revision.
- The submit-repo copies are byte-identical to the entry-dir originals (same sha256 for both solve.js and main.ts, verified 2026-11-23 03:46 WIB).

## Verification
- Practice set, final re-run on the exact submit-repo copies (`node verify.mjs ./site-generator-speed-01-run-20261122-kit ./submit-repo 3`): **3/3 cases identical** to makefun-site 1.0.0 (byte-for-byte vs `practice/reference/expected.json`), measured three times on this shared machine:
  - Main agent run 1 (03:44 WIB): mine 196.2 / 222.2 / 223.1 ms (median 222.2) vs house baseline 451.1 / 454.4 / 485.1 ms (median 454.4) — **2.05x faster**.
  - Finish-up agent re-run (03:46 WIB): mine 284.2 / 327.3 / 349.4 ms (median 327.3) vs house baseline 453.3 / 463.5 / 490.9 ms (median 463.5) — **1.42x faster**.
  - Main agent run 2 (03:50 WIB): mine 211.2 / 227.5 / 422.3 ms (median 227.5) vs house baseline 452.4 / 465.2 / 472.3 ms (median 465.2) — **2.04x faster**.
  - Per-case timings vary run to run on this shared machine; the entry is consistently faster, **1.4–2.3x** across measurements.
- Speed on the full practice set, build agent's 5-run measurement: **~1,350 ms vs ~3,100 ms for the house baseline — about 2.3x faster**.
- Fresh generator-drawn sets (kit's own `draw.ts`, 3 seeds): **9/9 cases identical**, 2.6–2.9x faster.
- Differential fuzz vs the vendor baseline: **1,100 random nasty sites, 0 mismatches**.
- Determinism: `main.ts` end-to-end over the practice set run twice → byte-identical `answers.json` (sha256 25980928b145f54712027939364a64c277098bc4528a2d524e0bc27a0275fb03), 3/3 match expected.
- Docker is NOT available on this machine, so the kit's `grade-local` reproduce could not be run; verification rests on the local harness above. (Caveat.)

## Notes
- This kit ships NO `starter/` directory (unlike the tiny-stack-vm kit).
- The repo LICENSE is a byte-identical copy of the kit vendor makefun-site MIT LICENSE, with an `SPDX-License-Identifier: MIT` line prepended — the kit's license check requires that line (license text alone does not count).
- Sizes: solve.js 35,761 B; main.ts 1,441 B; README.md 1,368 B; LICENSE 1,095 B; BUILD_LOG.md 3,417 B; .makefun/owner.json 56 B. Total 43,138 B — well under the 4 MiB cap.

## Repo
- https://github.com/Kuyukbot1/site-generator-speed-01-run-20261122
