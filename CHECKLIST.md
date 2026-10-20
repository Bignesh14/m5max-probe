# Checklist — Phase 1 (M5 Max measurement)

Lives in the repo (not iCloud). `git pull` before reading.

Legend: [x] done · [ ] todo · (!) open question

## Done
- [x] 20 Oct — Repo cloned outside iCloud at ~/dev/m5max-probe on Studio and Air; checklist moved into the repo
- [x] 20 Oct — Air sysctl saved; diff: 26 Studio-only lines (SME family, MTE, CSSC, HBC, WFxT…), 1 Air-only (SSBS)
- [x] 20 Oct — Air vs LLVM apple-m3: SSBS matches (no mismatch)
- [x] 20 Oct — GitHub App installed; first commit pushed (README + data/sysctl)
- [x] 18 Oct — Studio sysctl + feature list saved (data/sysctl/studio_*)
- [x] 18 Oct — Studio features vs LLVM apple-m5: match except SPECRES/SPECRES2 (LLVM yes, macOS 0)
- [x] 18 Oct — Repo created: github.com/Bignesh14/m5max-probe; Claude can read, not push yet
- [x] 16 Oct — Phase 0: Studio setup, SSH, Homebrew, LLVM/MLIR source build started
- [x] 17 Oct — Plan reviewed → MASTER_PLAN_v2.md (Learn2 folder)
- [x] 17 Oct — LLVM finding: apple-m5 exists, uses CycloneModel (2013 A7), CacheLineSize defaults to 64
- [x] 17 Oct — Prior work found: m5-uarch (base M5 only; no M5 Max, no line size, no bandwidth, no SME)
- [x] 18 Oct — Step 1: sysctl on Studio. 6 Super + 12 Performance; L2 per 6 cores; cachelinesize 128; page 16 KiB

## Next
- [~] Step 2a: concept — CPU cycle vs time (in progress)
- [ ] Step 2: instrumentation check (thread_selfcounts, Instruments, kpc)
- [ ] Step 3: core steering via QoS
- [ ] Step 4: pointer-chase latency vs size (both core types) → first blog chart
- [ ] Step 5: cache line size (stride test)
- [ ] Step 6: TLB · Step 7: prefetcher · Step 8: bandwidth
- [ ] ~20 Nov: email Sanchari Sen

## Open questions (!)
- (!) Is the 128 B line real for L1, or only for L2/coherence? → step 5
- (!) Default of enable_loop_data_prefetch on AArch64
