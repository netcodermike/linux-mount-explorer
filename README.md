# Linux Mount Explorer

Inspect the current Linux mount namespace with filesystem types, sources, parent IDs, and options.

[![Build and verify](https://github.com/netcodermike/linux-mount-explorer/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/linux-mount-explorer/actions/workflows/verify.yml)

**Language:** Rust · **Platform:** Linux · **App type:** Linux mount topology and filesystem inspector

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- /proc/self/mountinfo parsing
- Mount parent IDs
- Kernel path escape decoding
- Optional path substring filter

## Requirements

Rust stable, Linux, and the documented system data sources. No external crates.

## Quick start

```sh
git clone https://github.com/netcodermike/linux-mount-explorer.git
cd linux-mount-explorer
cargo run --release
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Run cargo run --release, then pass /proc as a substring filter and compare IDs/types with /proc/self/mountinfo.

## Architecture, configuration, and data

src/main.rs splits mountinfo at the mandatory separator, parses mount/parent IDs and root/path/options, then displays filesystem type and source. It decodes the kernel’s four common octal path escapes and escapes control characters for terminal display. Tests cover parent IDs, filesystem type, malformed rows, and escaped spaces. No mounts are created or changed.

## Verification

Build with the quick-start command where needed, then run:

```sh
cargo test
```

Manual acceptance: Run cargo run --release, then pass /proc as a substring filter and compare IDs/types with /proc/self/mountinfo. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

Current namespace only; no mount/unmount, privilege changes, full graphical topology, capacity statistics, or continuous monitoring. Optional propagation fields and superblock options are not displayed. Missing/changed rows during sampling can be skipped. This is an inspector, not a filesystem health check.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `Cargo.toml`
- `src/main.rs`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
