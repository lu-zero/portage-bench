# portage-bench

Benchmarks comparing Gentoo Portage parsing libraries.

## What's Benchmarked

### Synthetic Dependencies (`dep_parsing`)

Parses dependency strings of increasing complexity through `portage-atom::DepEntry::parse` and `pkgcraft::DependencySet::package`:

| Input | Description |
|-------|-------------|
| `simple` | Single atom: `dev-libs/openssl` |
| `medium` | Flat list with USE conditionals |
| `complex` | Nested groups, blockers, slot operators |

Also benchmarks `portage-metadata::RequiredUseExpr::parse` and a direct comparison group.

### Real-world Dependency Sets (`realworld_dep_parsing`)

Parses full `DEPEND`/`RDEPEND` strings from real Gentoo ebuilds:

| Package | Lines | Why |
|---------|-------|-----|
| `texlive` | ~100 | Heavily USE-conditional with many l10n flags |
| `pandoc` | ~30 | Moderate complexity |
| `ffmpeg` | ~70 | Deep nesting, many operators |

## Libraries Under Test

- [portage-atom](https://crates.io/crates/portage-atom) — lightweight PMS atom and dependency parser
- [portage-metadata](https://crates.io/crates/portage-metadata) — ebuild metadata cache types and parser
- [pkgcraft](https://github.com/pkgcraft/pkgcraft) — full-featured Gentoo package manager library

## Setup

This repo uses path dependencies for pkgcraft. Clone it alongside the other portage crates:

```
git clone https://github.com/lu-zero/portage-bench
cd portage-bench
git clone https://github.com/pkgcraft/pkgcraft ../pkgcraft
cargo bench
```

## Running

```bash
# All benchmarks
cargo bench

# Only synthetic
cargo bench --bench dep_parsing

# Only real-world
cargo bench --bench realworld_dep_parsing

# Compare against a saved baseline
cargo bench -- --baseline <name>
```

## License

[MIT](LICENSE-MIT)
