# StructOpt — Stability Layer for Optimization

This repository demonstrates **StructOpt**, a structural stability layer
for first-order optimization methods.

The goal is not to compete on raw convergence speed,
but to isolate and demonstrate a qualitative property:

> **StructOpt suppresses oscillations and prevents divergence
> in stiff or ill-conditioned optimization regimes.**

---

## Motivation

Many optimization problems exhibit unstable dynamics:
large gradients, oscillatory trajectories, or exploding loss values.

Standard optimizers:
- **SGD** diverges under fixed step size,
- **Adam** partially stabilizes but retains oscillations.

StructOpt introduces a **structural signal S(t)** that dynamically rescales
the effective update, acting as a stability controller.

---

## Stability Stress Test (Main Result)

![Stability Stress Test](figures/fig2_structopt_stability_stress.png)

**Test description:**
- Fixed learning rate
- Oscillatory / stiff objective
- No second-order information

**Observed behavior:**
- SGD: divergence and limit-cycle dynamics
- Adam: partial damping, residual oscillations
- StructOpt: smooth convergence to equilibrium

This demonstrates StructOpt as an effective **stability layer**.

---

## Mechanism: Structural Signal Control

![Structural Signal Mechanism](figures/fig1_structopt_mechanism.png)

The structural signal **S(t)** increases automatically when instability is detected.

This reduces the effective step size via:

\[
\Delta x \sim \frac{1}{S(t)}
\]

No tuning, curvature estimates, or line search are required.

---

## Key Insight

StructOpt separates:
- **direction** (gradient)
- **stability** (structural signal)

This decoupling allows stable optimization in regimes
where classical methods fail.

---

## Status

This is a research prototype intended to demonstrate
a qualitative stability effect.

Further benchmarks and extensions are left for future work.
