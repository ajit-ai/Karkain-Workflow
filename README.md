# Karkain-Workflow

Stateful workflow step orchestration for Karkain

- **Language baseline:** Karkain Language v1.2.0 (verified tag `v1.2.0`, commit `77d70693e1e3134dac312a303bffafa7d50fa988`).
- **Framework version:** `0.1.0-dev`.
- **Status:** VERIFIED - module, native tests, integration and example executed with the real compiler.
- **Repository model:** independent repository; no submodules, no framework dependencies unless explicitly documented.

## Purpose

Stateful workflow step orchestration for Karkain The framework is implemented in the verified canonical Karkain v1.2.0 subset: untyped functions, `let`, `while`, `if`/`else`, arrays, strings and documented builtins. Top-level structs are unavailable in this subset, so state is represented with documented primitive/array conventions and every mutating function returns the updated value.

## Public API

Module: `src/workflow.kark` (import as `workflow`). See the source file for function contracts and the array representation convention.

## Layout

`	ext
src/workflow.kark          framework implementation
src/verify.kark           integration program
tests/api_tests.kark      native test_* bodies
examples/                 runnable example
scripts/verify.ps1        verification gate
COMPATIBILITY.md          evidence-based baseline assessment
karkain.toml              project manifest (version 0.1.0-dev)
`

## Verification

`powershell
powershell -ExecutionPolicy Bypass -File scripts\verify.ps1
`

Gates: module `check`; 8 native tests; integration `run`; a negative gate proving exit code 4; and a runnable example. Because `karkain test` cannot resolve imports, the native test program is generated from the real module source plus test bodies in a temporary directory.

## Dependencies

None, unless stated otherwise in the source documentation.

## Limitations

Verified v1.2.0 boundaries apply: array value semantics, integer 1/0 comparison results, no top-level structs, no logical `and`/`&&`, and no `import` support in `karkain test`. No cross-platform, WASM, GPU, NPU, quantum, networking or database support is claimed unless actually exercised. See `COMPATIBILITY.md`.