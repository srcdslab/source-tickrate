# Changelog

This is the srcdslab fork of [angelfor3v3r/source-tickrate](https://github.com/angelfor3v3r/source-tickrate).
Fork versions are `X.Y.Z-srcdslab`, starting after upstream 1.4.5.

## [1.4.6-srcdslab] - 2026-11-21

### Changed

- CI rewritten to follow the srcdslab conventions (`.github/workflows/ci.yml`):
  - a push to the default branch replaces the `latest` release, a pushed tag creates a release on
    that tag; the upstream `RELEASE_TOKEN` secret is no longer needed;
  - one archive per OS and architecture, `source-tickrate-<version>-<os>-<arch>.tar.gz`
    (`<version>` is `latest` or the tag), extracting straight into the game folder
    (`addons/tickrate_<arch>.{so,dll}` + `addons/tickrate_<arch>.vdf`);
  - pull requests build and package too (workflow artifacts), without releasing.
- Linux builds run in an `ubuntu:20.04` container (glibc 2.31) instead of `debian:buster`, whose apt
  mirrors are gone. The CI fails if a Linux `.so` needs a glibc newer than 2.31.
- Windows builds pinned to `windows-2022` (Visual Studio 17 2022).
- The plugin description (`plugin_print`) now shows the version: `Tickrate 1.4.6-srcdslab (angelfor3v3r)`.
- CMake project version set to `1.4.6`.

### Fixed

- The Linux library now links `libdl` (`dlopen`, `dlinfo`, `dlsym`, `dladdr`, `dlclose`), which
  lives outside libc before glibc 2.34. It only loaded before because the server had already
  loaded `libdl`.

### Added

- Dependabot for GitHub Actions, with auto-merge of its pull requests.

## 1.4.5 and earlier

See the [upstream releases](https://github.com/angelfor3v3r/source-tickrate/releases).
