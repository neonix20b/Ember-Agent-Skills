# Ports and current development tools

Read this for third-party software, dependency upgrades, or build failures.
The owning source of recipes and validation is
[EmberBSD-Ports](https://github.com/neonix20b/EmberBSD-Ports), not this skill.

## Choose and pin the source

- Verify the current stable upstream release from an original release page.
  Distinguish a supported LTS choice with a concrete reason from an obsolete
  package retained merely because it builds. Record the verification date.
- Check the pinned pkgsrc base and current pkgsrc/pkgsrc-wip before writing a
  new recipe. Reuse their relevant work and preserve authorship and licenses.
  Pin the exact revision; do not build an unrecorded moving HEAD.
- Keep original download URLs, versions, SHA256, recipe parameters, and patch
  provenance in Ports. Verify archives before extraction. A mismatch is an
  error to investigate, not a reason to replace the expected hash.
- Keep the small delta over pkgsrc. Use ordinary package recipes, dependency
  declarations, staging and package tools; do not invent another package manager.
  Upstream trees, archives, caches and binaries stay outside Git history.
- Fix source, recipe and ABI incompatibilities in versioned Ports sources.
  A repair left only inside a build VM is incomplete.

## Keep the development profile coherent

Current EmberBSD development profiles include current stable compilers and build
tools, plus Ruby, Go and TinyGo. Recheck versions for each upgrade; a version
listed in an old conversation is not a permanent pin.

Build the new compiler with a recorded bootstrap compiler, then rebuild its
affected dependency closure. A temporary bootstrap or recovery compiler is not
the final image's default development environment. Changes to the system image
and base toolchain belong to the OS repository and need their own checks.

For C++ libraries, inspect both DT_NEEDED and the runtime actually loaded.
Do not disguise one libstdc++ SONAME as another. Do not accept two C++ runtimes
in one process. Test object exchange, exception unwinding and representative
consumers such as Qt or LLVM after a compiler/runtime change.

Choose current common dependencies and adapt their consumers. If an upstream
requires a private fork, inspect its patches and supported targets before
replacing it with a shared library. Preserve functionality rather than silently
dropping a backend to make the build green. Document any temporary restriction
and its removal condition; do not label the restricted result fully supported.

## Test what a developer will use

| Change | Useful acceptance evidence |
| --- | --- |
| C/C++ compiler | Compile, link and run code with atomics, threads, TLS, and shared-library exception boundaries; inspect actual runtime resolution |
| Ruby | Run Ruby and package tests; build and load a native extension using the selected compiler |
| Go | Build and test a module, including cgo where supported; record bootstrap and actual compiler paths |
| TinyGo | Build a Wasm/WASI program and run it with a compatible runtime; separately compile selected MCU targets and distinguish compilation from flashing or a board test |
| Ordinary port | Upstream tests, regression for each local fix, staged package/install checks and a meaningful user workflow |
| Shared library | Affected direct and transitive consumers, loader identity, clean shutdown and repeated use where lifetime changed |

Keep real exit statuses. Do not accept stale output from a failed build, suppress
unexplained warnings, replace unavailable behavior with success stubs, or report
a skipped device test as a pass. Record the revision, configuration, commands,
results and artifact hashes. Full logs may stay in a private artifact store;
include enough non-sensitive evidence to reproduce the result publicly.

Coordinate shared build machines before changing compilers, libraries or VM
configuration. Measure free disk and RAM, limit workers, and retain a recovery
path. Reboots and device writes must be within the task's authorized scope.

## Verified lessons to recheck when they apply

- **TinyGo from pkgsrc-wip:** revision
  [30b5c392](https://github.com/NetBSD/pkgsrc-wip/tree/30b5c39233c7affa55f3db0a692457e16c127181/tinygo)
  packages 0.42.0 with NetBSD adaptations and a bundled LLVM fork.
  The [0.42.0 release](https://github.com/tinygo-org/tinygo/releases/tag/v0.42.0)
  supports Go 1.27 and LLVM 22. Checked 2026-10-06. LLVM 23 compatibility and
  native EmberBSD execution require testing; recipe presence proves neither.
- **Graphics evidence:** software EGL readback, KMS scanout, native Wayland
  input, and host GPU rendering are separate claims. See the current
  [Wayland probe](https://github.com/neonix20b/EmberBSD-Ports/tree/main/probes/wayland-utm)
  for its exact tested limits. A nested desktop or software renderer cannot
  establish hardware acceleration.

When those sources advance, recheck the affected case and update this reference.
Keep detailed recipes and executable regressions with their owning port.
