# Dynamic Mode Decomposition of Power-System Forced Oscillations

MATLAB project applying **Dynamic Mode Decomposition (DMD)** to PMU measurements from a
29-generator power system, to identify the modes behind a forced oscillation event: their
frequencies, damping ratios, amplitudes, energy, and which generators participate in each mode.

## Method

```text
PMU frequency data (29 generators, 40 s @ 1200 Hz)
  → demean & build snapshot matrices X₁, X₂
  → economy SVD (rank selection, forced rank 29)
  → regularized exact DMD   (Ã = Φ⁻¹AΦ + λ·I regularization)
  → eigen-decomposition → modes
  → amplitudes b = Φ⁺x₁  → time-domain reconstruction (relative Frobenius error)
  → mode analysis: frequency, damping, energy, amplitude,
    per-generator participation, dominant generator
  → plots: singular-value spectrum, polar mode shapes
```

## Files

`EEE_1.mlx` … `EEE_6.mlx` are successive iterations of the same MATLAB live script — **`EEE_6`
is the latest** (later versions add robustness around data loading and mode analysis). Each is
self-contained, with local functions `load_data`, `analyze_modes`, and `calc_participation`.

## Data requirement

The scripts load the **forced-oscillation test case** (Case 1F) from a PMU
TestCasesLibrary-style dataset: 40 seconds of frequency measurements at 1200 Hz for 29
generators. The dataset is **not included** — download a forced-oscillation case library and
point `data_folder` (top of the script) at its `Case 1F` folder, then run the live script.

## Requirements

- MATLAB (base) — the scripts use SVD/eig/tables only
- Signal Processing Toolbox for some plots in later iterations
