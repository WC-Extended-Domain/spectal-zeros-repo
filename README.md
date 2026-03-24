[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/) 
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Zenodo](https://img.shields.io/badge/zenodo-2501.xxxxx-b31b1b.svg)](https://zenodo.org/abs/2501.xxxxx)
[![DOI](https://img.shields.io/badge/DOI-10.1234%2Ftsqvt-blue)](https://doi.org/10.1234/tsqvt)
[![Documentation](https://img.shields.io/badge/docs-latest-brightgreen.svg)](https://tsqvt.readthedocs.io/)




<p>
  <a href="https://github.com/WC-Extended-Domain/spectal-zeros-repo">
    <img src="https://github.com/WC-Extended-Domain/spectal-zeros-repo/blob/main/spectral-zeros-repo.png?raw=true" 
         alt="Research Status" 
         width="97" 
         align="left" />
  </a>
  <h1 style="display: inline;">
    Spectral Detection of Automorphic<br> & Arithmetic Zeros
  </h1>
</p>
<h2 style="display: inline;">
    Transfer Operators, Scattering Theory, and Fixed-Point Diagnostics for L-functions
  </h2>


---

## Overview

Two independently verified spectral methods for detecting zeros of L-functions, each anchored to a **rigid mathematical identity** requiring no parameter fitting:

### Part I: Mayer–Ruelle Transfer Operator → Maass Cusp Forms

The transfer operator L_s for the Gauss map, with matrix elements M_{jk}(s) = (-1)^j / j! · (2s+k)_j · ζ(2s+k+j), detects the first four Maass spectral parameters (r₁ through r₄) with up to six-digit precision at basis truncation K=35. The Lewis–Zagier factorisation correctly discriminates even and odd Maass forms.

### Part II: Eisenstein Scattering → Riemann Zeta Zeros

The scattering coefficient φ(s) = ξ(2s−1)/ξ(2s) detects all first 10 non-trivial Riemann zeta zeros as poles, with average error 9.2×10⁻⁴ at scan resolution Δt=0.005, refining to 10⁻⁷ via bisection.

### Fixed-Point Diagnostic (Negative Result)

The fixed points of the zeta map (attractor s₋ ≈ −0.296, repulsor s₊ ≈ 1.834) explain why composition operator constructions fail: the spectral structure is governed by fixed-point dynamics, not by the zeros.

## Installation

```bash
git clone https://github.com/AGE-Quantum/spectral-zeros.git
cd spectral-zeros
pip install -e ".[dev]"
```

## Quick Start

```python
from spectral_zeros import detect_maass, pole_scan, match_zeros, find_zeta_fixed_points

# Detect first Maass cusp form
result = detect_maass(9.5337, K=25)
print(f"|λ−(−1)| = {result['dist_minus1']:.2e}")  # Even form → target -1

# Detect Riemann zeros via Eisenstein scattering
poles = pole_scan(10.0, 55.0, dt=0.01)
matches = match_zeros(poles)
print(f"Found {len(matches)}/10 zeros")

# Fixed-point diagnostic
fp = find_zeta_fixed_points()
print(f"Attractor: s₋ = {fp['s_minus']:.4f}, |ζ'| = {fp['deriv_minus']:.3f}")
```

## Running the Verification Suites

```bash
# Selberg–Mayer verification (~4–5 minutes)
python scripts/verify_all.py

# Eisenstein scattering verification (~30 seconds)
python scripts/adelic_verification.py
```

## Tests

```bash
pytest tests/ -v
```

## Repository Structure

```
spectral-zeros/
├── src/spectral_zeros/
│   ├── mayer_ruelle.py        # Mayer matrix, inverse iteration, Maass detection
│   ├── eisenstein.py           # Scattering coefficient, pole scan, bisection
│   └── fixed_points.py         # Zeta map fixed points
├── scripts/
│   ├── verify_all.py           # Full Selberg–Mayer suite (T1–T5)
│   └── adelic_verification.py  # Full Eisenstein suite (T1–T5)
├── tests/
│   └── test_spectral_zeros.py  # Unit + integration tests
├── docs/
│   └── Automorphic_and_Arithmetic_Zeros_v2.tex  # Paper source
└── pyproject.toml
```

## Audit Protocol

Every claimed detection must pass: (A1) K-convergence, (A2) negative controls, (A3) parity/target discrimination, (A4) precision scaling, (A5) deterministic reproducibility.

## Citation

```bibtex
@article{Makraini2026spectral,
  title   = {Spectral Detection of Automorphic and Arithmetic Zeros
             via Transfer Operators and Scattering Theory},
  author  = {Makraini, Kerym},
  year    = {2026},
  note    = {UNED / AGE Quantum Gates Engine S.L.}
}
```

## License

MIT
