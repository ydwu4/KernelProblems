# v8 benchmark comparison

Consolidated from 20 per-problem `benchmark.json` files. The [consolidated JSON](benchmark_comparison.json) retains every original entry and field.

`simple_prompt_kernel` has a lower recorded time than the fastest passing alternative in 17 of 17 problems with usable alternatives. The geometric mean of the recorded best-other/simple ratios is 4.12x. 3 problems have no passing alternative timing.

- This report reads only v8/*/benchmark.json; it does not run or retime kernels.
- Time ratios use the stored time_ms values. Earlier backend entries omit hardware, software, and timing-method metadata, so common measurement conditions are unverified.
- PASS, tol_tier, errors, notes, and failure reasons are preserved as reported. Some historical entries labeled bitwise have nonzero max_abs_err. Neither that label nor a zero numerical error alone proves raw-byte parity.
- Ratios include only PASS entries with finite positive timings. Missing, failed, errored, or skipped alternatives do not count as timing wins.
- Memory and roofline findings appear in simple_prompt_kernel notes; the other entries do not contain corresponding measurements for a quantitative comparison.

All times below are stored values in milliseconds. “Best other / simple” uses the fastest passing non-simple backend; eager is shown separately.

| Problem | eager_ms | kernelagent_triton | kernelagent_triton_opt | torch_compile | torch_compile_max_autotune | simple_prompt_kernel | Best other / simple |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [12545c1e9b06](12545c1e9b06/benchmark.json) | 1.764943 | 0.523399 | 0.520038 | 0.290503 | 1.591346 | 0.067933 | 4.28x |
| [385e1beb9bb9](385e1beb9bb9/benchmark.json) | 0.945019 | 0.635482 | 0.630485 | 0.624390 | 1.676725 | 0.197077 | 3.17x |
| [3c6c589cdf81](3c6c589cdf81/benchmark.json) | 0.668178 | 0.387405 | 0.245695 | 0.290313 | 0.581788 | 0.101069 | 2.43x |
| [43f0c930291e](43f0c930291e/benchmark.json) | — | FAIL | SKIP | ERROR | ERROR | 0.106206 | — |
| [493cad38cac9](493cad38cac9/benchmark.json) | 0.551228 | 0.161767 | 0.090036 | 0.407614 | 0.395557 | 0.018328 | 4.91x |
| [4b90e2d83144](4b90e2d83144/benchmark.json) | 0.202886 | 0.104731 | 0.102200 | 0.185122 | 0.256729 | 0.020507 | 4.98x |
| [622c35f5d1c6](622c35f5d1c6/benchmark.json) | 12.149397 | 2.911875 | SKIP | 3.003288 | 6.798575 | 0.866768 | 3.36x |
| [71f1d2c9f38b](71f1d2c9f38b/benchmark.json) | 10.970360 | 1.840799 | 1.840914 | 1.368699 | 3.150474 | 0.517579 | 2.64x |
| [7815074de963](7815074de963/benchmark.json) | 1.735779 | 1.142408 | 1.121681 | 0.416879 | 1.034444 | 0.124370 | 3.35x |
| [7884328a5557](7884328a5557/benchmark.json) | 0.290308 | 0.095053 | 0.095066 | 0.181305 | 0.268239 | 0.027840 | 3.41x |
| [7e38211c7f1c](7e38211c7f1c/benchmark.json) | 0.035787 | MISSING | MISSING | MISSING | MISSING | 0.004478 | — |
| [8e33a91b7364](8e33a91b7364/benchmark.json) | 1.486722 | 1.052649 | 1.052414 | 1.049323 | 2.378080 | 0.328093 | 3.20x |
| [94985bdb7630](94985bdb7630/benchmark.json) | 1.764277 | 0.508009 | 0.402570 | 0.416858 | 1.038955 | 0.124398 | 3.24x |
| [97032595d968](97032595d968/benchmark.json) | 1.349655 | 0.411258 | 0.143351 | 0.915846 | 0.493667 | 0.025894 | 5.54x |
| [c68dae22972b](c68dae22972b/benchmark.json) | 0.533863 | 0.316062 | 0.317194 | 0.316972 | 0.849736 | 0.097621 | 3.24x |
| [c8c60d8f7015](c8c60d8f7015/benchmark.json) | 1.372121 | 0.204628 | 0.143210 | 0.915960 | 0.493297 | 0.026008 | 5.51x |
| [d8f596b3df34](d8f596b3df34/benchmark.json) | 0.505044 | 0.321923 | 0.210916 | 0.370622 | 0.441228 | 0.082328 | 2.56x |
| [e29b92927600](e29b92927600/benchmark.json) | 0.549294 | 0.094882 | 0.095904 | 0.402373 | 0.264225 | 0.004517 | 21.01x |
| [f4e9e58fef73](f4e9e58fef73/benchmark.json) | 0.176888 | 0.130755 | 0.129021 | 0.192954 | 0.248919 | 0.020432 | 6.31x |
| [f6251e84e3fa](f6251e84e3fa/benchmark.json) | — | FAIL | SKIP | ERROR | ERROR | 0.442653 | — |

Status counts cover all problems, including missing entries. “Zero error” counts PASS entries reporting `max_abs_err == 0`; it is not a separate bitwise validation.

| Backend | PASS | FAIL | ERROR | SKIP | MISSING | Timed PASS | Zero error | Bitwise label with nonzero error |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `kernelagent_triton` | 17 | 2 | 0 | 0 | 1 | 17 | 2 | 4 |
| `kernelagent_triton_opt` | 16 | 0 | 0 | 3 | 1 | 16 | 3 | 3 |
| `torch_compile` | 17 | 0 | 2 | 0 | 1 | 17 | 5 | 3 |
| `torch_compile_max_autotune` | 17 | 0 | 2 | 0 | 1 | 17 | 5 | 3 |
| `simple_prompt_kernel` | 20 | 0 | 0 | 0 | 0 | 20 | 20 | 0 |

Recorded ratios use `other["time_ms"] / simple_prompt_kernel["time_ms"]`; values above 1 mean the simple entry has the lower stored time. Each row uses only its own paired problems, with unrounded timings for arithmetic.

| Other backend | Paired problems | Geomean recorded ratio | Minimum | Maximum | Simple lower / tied / higher |
| --- | --- | --- | --- | --- | --- |
| kernelagent_triton | 17 | 5.55x | 3.21x | 21.01x | 17 / 0 / 0 |
| kernelagent_triton_opt | 16 | 4.70x | 2.43x | 21.23x | 16 / 0 / 0 |
| torch_compile | 17 | 7.04x | 2.64x | 89.08x | 17 / 0 / 0 |
| torch_compile_max_autotune | 17 | 11.35x | 5.36x | 58.50x | 17 / 0 / 0 |
| Best passing other | 17 | 4.12x | 2.43x | 21.01x | 17 / 0 / 0 |
| eager_ms (stored) | 18 | 14.17x | 4.53x | 121.61x | 18 / 0 / 0 |

Problems without a passing alternative retain the following recorded outcomes:

- `43f0c930291e` — `kernelagent_triton`: FAIL, `kernelagent_triton_opt`: SKIP, `torch_compile`: ERROR, `torch_compile_max_autotune`: ERROR. Reasons: execution (trial 0): index 1 is out of bounds for dimension 0 with size 0; no optimized_kernel.py.
- `7e38211c7f1c` — `kernelagent_triton`: MISSING, `kernelagent_triton_opt`: MISSING, `torch_compile`: MISSING, `torch_compile_max_autotune`: MISSING.
- `f6251e84e3fa` — `kernelagent_triton`: FAIL, `kernelagent_triton_opt`: SKIP, `torch_compile`: ERROR, `torch_compile_max_autotune`: ERROR. Reasons: execution (trial 0): index 1 is out of bounds for dimension 0 with size 0; no optimized_kernel.py.
