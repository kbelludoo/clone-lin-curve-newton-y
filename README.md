# clone-lin-curve-newton-y

Experimental **LIN** clone of Curve Finance tricrypto
`CurveCryptoMathOptimized3._newton_y` (Newton fallback for `y` given the other
two scaled balances and invariant `D`).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [curvefi/tricrypto-ng](https://github.com/curvefi/tricrypto-ng) `ecaa8161c240f21dd7c3712eefc5637e1dac742b`
  - `contracts/main/CurveCryptoMathOptimized3.vy` sha256 `d0d48e5c3fa00e36f841250cbce8665292ba3224bb050c948dc3b12a50f01d6c` blob `695c794cb8035e4b2848ad0354d0993dcfb9c7cb`
  - Curve.Fi publishes that tree as informational-only (no reproduction license). This repository does **not** vendor the Vyper source.
- **LIN kernel:** [`src/lin_curve_newton_y.lin`](src/lin_curve_newton_y.lin) (sha256 `118b1c0b343d3ab5f7bf51c1f420b88c27350e9a23fbd4ba7068a370f11ae287`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/curve_newton_y_c11.c`](test/oracles/curve_newton_y_c11.c)
- **Proofs (lin-open only):** `examples/curve_newton_y/` and `make curve-newton-y-proof`
- **Class:** EXPERIMENTAL uint64-scale, `SCALE = 1e9`. Not Ethereum tricrypto uint256. Not `price_scale` / `newton_D` / analytic `get_y` cubic. Not a production pool replacement.

Named goldens (equal `1e9` balances, `ANN=1707629`, `gamma=11809`): identity **1000000000**; `x0 += 10%` → `y1` **909085543**; `get_dy` +10% no-fee **90914456**; 0.03% fee **90887181**; `dx=0` fail-closed **0**; `ANN=MIN_A=2700` fail-closed **0** (`mul1` exceeds signed i64). Naive i64 `3e9 * 169349010160880` wraps to **5251948605238943744**.

## Reproduce proofs (in lin-open)

```bash
make curve-newton-y-proof
# or: python3 test/prove_curve_newton_y_external.py
```

## Not claimed

Uint256 / ONE=1e18 / price_scale mainnet parity. Analytic `get_y` / `cbrt`.
LIN replacing Curve or the EVM. TVL or dollar savings. zk soundness.
Stableswap `get_y` / `get_dy` (see clone-lin-curve-gety / clone-lin-curve-getdy).
