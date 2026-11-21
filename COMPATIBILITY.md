# Karkain v1.2.0 Compatibility Evidence (Karkain-Workflow)

## Baseline identity (verified)

| Item | Verified value |
|---|---|
| Source repository | `https://github.com/ajit-ai/Karkain` |
| Release tag | `v1.2.0` (annotated) |
| Tag object SHA | `e900c91e485fc316f52b664228f6c35f25416436` |
| Commit SHA | `77d70693e1e3134dac312a303bffafa7d50fa988` |
| Compiler | `Karkain Compiler v1.2.0 (windows/amd64, Stable Build)` |
| Release archive | `karkain-v1.2.0-windows-amd64.zip`, SHA-256 `f23b07f1a6b5ecd154615415ded1cd9e9bab2eb09b1c3e1e58200565e6d47001` (matched published `checksums.txt`) |

The compiler was downloaded from the official v1.2.0 release, checksum-verified, and run against a matching read-only source checkout at the `v1.2.0` tag. The Karkain Language repository was not modified.

## Verified language features used

`func`, untyped parameters, `let`, `return`, `while`, `if`/`else`, arrays (`[]`, `len`, `push`, indexing), strings (`+`, `len`, indexing, `contains`, `str`, `println`), comparisons, `assert`/`assert_eq`, `public func` exports, sibling-module `import` with qualified calls, and the `check`/`run`/`build`/`test` commands.

## Verified semantics and boundaries

- Arrays are values: mutating helpers return the updated array and callers capture it.
- Comparisons produce integer `1/0`; truth checks use `if ok` / `if ok == false`.
- No top-level `struct`; state uses documented primitive/array conventions.
- No logical `and`/`&&`; multi-condition logic uses explicit branches.
- `karkain test` cannot resolve `import`; tests are assembled from the real module source in a temporary file.
- Local imports resolve from the entry file's directory; the verification script stages modules beside consumers.
- The test driver emits non-fatal Winsock linker diagnostics on this host; failure detection was independently verified (exit code 4 on `assert(false)`).

No claim is made about Linux, macOS, mobile, WASM, GPU, NPU, quantum, networking or database support unless explicitly exercised by this repository's tests.