# Validation

Authoring date: November 6, 2026. Host: Windows. Target: Linux.

## Local result

Target-platform source CI is recorded after publication. This host has Python, Node.js, and .NET; other native toolchains are verified through CI. No unobserved GUI/device behavior is claimed.

## Reproducible checks

The GitHub Actions workflow builds/runs the following on `ubuntu-latest`:

```sh
cargo test
cargo run --release -- --help
```

## Manual acceptance

Run cargo run --release, then pass /proc as a substring filter and compare IDs/types with /proc/self/mountinfo. Also test malformed inputs and an unwritable output destination.

A workflow file is not evidence of a passing run. Observed CI run links and source commits are recorded after publication. Native GUI, sound, sleep/resume, and platform permissions require direct target-platform acceptance even when model tests pass.

## Observed CI result

Passed: [target-platform build/check](https://github.com/netcodermike/linux-mount-explorer/actions/runs/42206835976). Source commit: `2e1b6f1cc901e129a66ae5dc7f14b81c323c1167`. Later documentation-only changes do not alter the tested implementation. The reproducible commands above identify test scope; native GUI/audio/permissions are not implied by compilation.
