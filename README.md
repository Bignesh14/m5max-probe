# m5max-probe

Measuring the memory system and ISA of the Apple **M5 Max** (Mac Studio, 36 GB),
with an **M3** (MacBook Air) as a baseline, and comparing what I measure against
what macOS reports and what LLVM assumes.

Every experiment: predict → measure → explain the gap. Raw output is kept as-is.

## Machines

| | Mac Studio | MacBook Air |
|---|---|---|
| Chip | Apple M5 Max (Mac17,14) | Apple M3 (Mac15,12) |
| Core types | 6 Super + 12 Performance | 4 Performance + 4 Efficiency |
| L1D (big / small core) | 128 KiB / 64 KiB | 128 KiB / 64 KiB |
| L2 | 16 MiB per 6 Super · 8 MiB per 6 Performance (×2 clusters) | 16 MiB per 4 P · 4 MiB per 4 E |
| `hw.cachelinesize` | 128 | 128 |
| Page size | 16 KiB | 16 KiB |
| SME streaming vector length | 512 bit | — (no SME) |
| macOS | 27.0.1 (26A434) | 27.0.1 (26A434) |

Source: `data/sysctl/` (raw `sysctl` output, 18 Oct 2026).

## Findings so far

1. LLVM's `apple-m5` CPU uses `CycloneModel` (the 2013 A7 scheduling model) and
   leaves `CacheLineSize` at its default of 64; macOS reports 128. Which one is
   physically right is still to be measured.
2. ISA: 26 feature lines are Studio-only (SME/SME2/SME2.1 family, MTE, CSSC, HBC,
   WFxT, SVE_B16B16, EBF16, FPACCOMBINE); 1 is Air-only (SSBS).
3. LLVM's `apple-m5` feature list matches macOS except SPECRES/SPECRES2
   (LLVM: present; macOS: 0 for user programs).

## Layout

- `data/` — raw measurements, never edited
- `src/` — benchmark sources (coming)
- `notes/` — write-ups

## Prior work

- [m5-uarch](https://github.com/useless-husband/m5-uarch) — base M5 (4 Super + 6 E) tables.
  This repo covers the M5 Max and its new Performance core.

License: MIT
