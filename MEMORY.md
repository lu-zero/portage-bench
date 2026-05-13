# portage-bench Memory

## Hardware

All benchmark results below are from an **Apple M2 Max**.

## portage-atom 0.7.0 vs pkgcraft (commit b9fb45eb1) — confirmed run

### Synthetic (`dep_parsing`)

| Benchmark | portage-atom | pkgcraft | portage-atom faster by |
|---|---|---|---|
| simple | 269 ns | 311 ns | 16% |
| medium | 1.31 µs | 1.55 µs | 18% |
| complex | 3.26 µs | 3.54 µs | 9% |

### Real-world (`realworld_dep_parsing`)

| Benchmark | portage-atom | pkgcraft | portage-atom faster by |
|---|---|---|---|
| texlive | 39.0 µs | 69.7 µs | 79% |
| pandoc | 17.8 µs | 29.6 µs | 67% |
| ffmpeg | 31.8 µs | 45.2 µs | 42% |

### Pre-optimization baseline (portage-atom 0.6, no perf work)

| Benchmark | portage-atom | pkgcraft | portage-atom faster by |
|---|---|---|---|
| simple | 370 ns | 290 ns | -28% (slower) |
| medium | 2.06 µs | 1.47 µs | -40% (slower) |
| complex | 4.80 µs | 3.47 µs | -38% (slower) |
| texlive | 58.0 µs | 69.3 µs | 16% |
| pandoc | 18.5 µs | 30.6 µs | 66% |
| ffmpeg | 58.7 µs | 45.0 µs | -30% (slower) |

## Notes

- pkgcraft is a local path dependency at `../pkgcraft/crates/pkgcraft`, commit `b9fb45eb1`
- Results should be re-verified on multiple platforms before publishing
