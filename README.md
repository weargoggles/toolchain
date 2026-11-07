# toolchain

Prebuilt binaries of tools that upstream ships only as source, so that every
environment (laptops, CI, cloud agent sessions) installs them in seconds
instead of compiling. Public on purpose: cloud setup scripts get no
credentials, so a private release would be unreachable exactly when it is
needed.

Nothing here is patched. Each release is the upstream crate at a pinned
version, built with `cargo install --locked`, plus a SHA-256 for every archive.

## Releases

Tags are `<tool>-v<version>`, e.g. `weave-v0.7.0`. Each carries
`<tool>-<version>-<target>.tar.gz` and a matching `.sha256` for:

| target | runner |
|---|---|
| `x86_64-unknown-linux-gnu` | ubuntu-22.04 (glibc 2.35, so older hosts still run it) |
| `aarch64-unknown-linux-gnu` | ubuntu-22.04-arm |
| `aarch64-apple-darwin` | macos-15 |

## Adding a version

Actions → the tool's workflow → Run workflow, with the upstream version. The
workflow builds, then creates the release. Rerunning for an existing version
replaces its assets.

## Tools

| tool | upstream | crates |
|---|---|---|
| weave | https://github.com/Ataraxy-Labs/weave (MIT) | `weave-driver`, `weave-cli` |
