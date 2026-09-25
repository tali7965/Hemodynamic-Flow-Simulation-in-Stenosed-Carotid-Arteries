# Hemodynamic Flow Simulation in Stenosed Carotid Arteries

[![Institution](https://img.shields.io/badge/Institution-Sharif%20University%20of%20Technology-blue.svg)](https://en.sharif.edu/)
[![Department](https://img.shields.io/badge/Department-Mechanical%20Engineering-darkred.svg)](http://mech.sharif.ir/)
[![Course](https://img.shields.io/badge/Course-Fluid%20Mechanics%20I-green.svg)](#)
[![Format](https://img.shields.io/badge/Report-PDF-red.svg)](Project-Report.pdf)

## Overview
This repository contains the computational fluid dynamics (CFD) investigation of hemodynamic flow through stenosed human carotid arteries. The study examines the fluid mechanical consequences of atherosclerotic plaque accumulation, focusing on trans-stenotic pressure gradients, velocity amplification, wall shear stresses, and hydraulic head loss across mild and moderate constriction severities.

- **Author:** Ali Taheri
- **Supervising Professor:** Dr. Kamran
- **Teaching Assistant:** Eng. Sajjad Fartash
- **Academic Year:** 2024–2025
- **Institution:** Department of Mechanical Engineering, Sharif University of Technology

---

## Deliverables & Repository Structure

The primary deliverable in this repository is the complete, publication-ready project report:

```text
├── Project-Report.pdf     # Full 15-page academic CFD engineering report
├── README.md              # Project summary and documentation
├── .gitignore             # Configured ignore rules
└── .source_backup/        # Archived LaTeX source (report.tex), figures, and assets
```

---

## Scientific Background & Clinical Significance
Carotid artery stenosis is caused by the progressive buildup of lipid-rich plaques beneath the endothelial lining of the carotid artery. Luminal narrowing induces:
1. **Convective Acceleration:** High velocities at the stenosis throat causing elevated wall shear stress (WSS), triggering platelet activation and endothelial denudation.
2. **Post-Stenotic Separation:** Recirculating and low-shear stagnation zones downstream favor thrombus formation and embolization (primary precursors to ischemic stroke).
3. **Hydraulic Resistance:** Substantial static pressure drop requiring elevated upstream driving pressures to maintain adequate cerebral perfusion.

---

## Numerical Methodology & Model Specifications

- **Solver:** ANSYS Fluent (Double precision, Pressure-based)
- **Pressure-Velocity Coupling:** SIMPLE algorithm
- **Spatial Discretization:** Second-Order Upwind scheme for momentum, Standard scheme for pressure interpolation
- **Convergence Criteria:** Continuity and momentum scaled residuals $< 10^{-4}$ (momentum $< 10^{-6}$)
- **Vessel Dimensions:** Unconstricted diameter $D = 3.5\text{ mm}$, total length $L = 61.6\text{ mm}$ ($L/D \approx 17.6$), centered stenosis throat at $x/L = 0.5$ ($L_{\text{stenosis}} = 6.0\text{ mm}$)

### Constriction Severities:
1. **Mild Occlusion (30% Stenosis):** Throat diameter $D_{\text{throat}} = 2.45\text{ mm}$ (70% open lumen)
2. **Moderate Occlusion (40% Stenosis):** Throat diameter $D_{\text{throat}} = 2.10\text{ mm}$ (60% open lumen)

### Fluid Thermophysical Properties:
| Parameter | Blood (Primary) | Glycerin (Parametric Study) | Ratio (Glycerin / Blood) |
| :--- | :---: | :---: | :---: |
| Density ($\rho$) | $1063.0\text{ kg/m}^3$ | $1259.9\text{ kg/m}^3$ | $1.185\times$ |
| Dynamic Viscosity ($\mu$) | $0.043\text{ Pa}\cdot\text{s}$ | $0.799\text{ Pa}\cdot\text{s}$ | $\mathbf{18.58\times}$ |
| Inlet Velocity ($u_{\text{in}}$) | $0.08\text{ m/s}$ ($8.0\text{ cm/s}$) | $0.08\text{ m/s}$ ($8.0\text{ cm/s}$) | $1.000\times$ |
| Outlet Pressure ($p_{\text{out}}$) | $11,999\text{ Pa}$ ($90\text{ mmHg}$) | $11,999\text{ Pa}$ ($90\text{ mmHg}$) | $1.000\times$ |
| Reynolds Number ($\text{Re}$) | $\sim 6.92$ | $\sim 0.44$ | $0.064\times$ |

---

## Key Findings

### 1. Velocity Amplification & Conservation of Mass
- **30% Stenosis:** Peak throat velocity increases from $0.08\text{ m/s}$ to **$0.32\text{ m/s}$** ($4.0\times$ amplification).
- **40% Stenosis:** Peak throat velocity increases from $0.08\text{ m/s}$ to **$0.43\text{ m/s}$** ($5.4\times$ amplification).
- Parabolic radial profiles are preserved across the throat cross-section, with steep velocity gradients concentrating elevated shear stress along the vessel wall.

### 2. Static vs. Dynamic Pressure Trade-Off
- Static pressure accounts for **$>99\%$** of total mechanical energy in the conduit.
- Dynamic pressure surges locally at the throat (from $3.4\text{ Pa}$ inlet up to $99\text{ Pa}$ in the 40% case), driving a steep static pressure drop via Bernoulli effect.
- Strong viscous dissipation prevents dynamic pressure recovery downstream, producing an irreversible total head loss.

### 3. Quantitative Hydraulic Loss Comparison
The non-dimensional hydraulic loss coefficient is defined as $\xi = \frac{\Delta p}{\frac{1}{2}\rho u_{\text{in}}^2}$:
| Occlusion Severity | Inlet Pressure $p_{\text{in}}\ [\text{Pa}]$ | Pressure Drop $\Delta p\ [\text{Pa}]$ | Loss Coefficient $\xi$ | Relative Increase |
| :--- | :---: | :---: | :---: | :---: |
| **Mild (30% Stenosis)** | $12,733.91$ | $734.91$ | **$216.07$** | Baseline |
| **Moderate (40% Stenosis)** | $12,796.60$ | $797.60$ | **$234.47$** | **$+8.51\%$** |

### 4. Grid Independence Verification
Spatial convergence was verified using coarse ($11,103$ elements), medium ($31,920$ elements), and fine ($119,356$ elements) grids:
- Discretization error between medium and fine grids is under **$1.88\%$**, validating mesh convergence for the baseline medium mesh.

### 5. Viscous Sensitivity (Glycerin Parametric Study)
- Substituting blood with glycerin ($\mu = 0.799\text{ Pa}\cdot\text{s}$) caused an **$18.43$-fold surge** in static pressure drop ($\Delta p = 14,703.3\text{ Pa}$ vs. $797.6\text{ Pa}$).
- This proportional scaling ($\Delta p \propto \mu \cdot u_{\text{in}}$) demonstrates strict Stokesian/Poiseuille viscous dominance over inertial effects at low Reynolds numbers ($\text{Re} \ll 100$).
- Loss coefficient increased to **$\xi = 3646.5$** ($15.55\times$ increase).

---

## References
1. **Fartash, S.** (2024). *Fluid Mechanics I Computational Laboratory Tutorials: Hemodynamic Flow Modeling in ANSYS Fluent*. Department of Mechanical Engineering, Sharif University of Technology.
2. **Ku, D. N.** (1997). Blood flow in arteries. *Annual Review of Fluid Mechanics*, 29(1), 399–434.
3. **Berger, S. A., & Jou, L. D.** (2000). Flows in stenotic vessels. *Annual Review of Fluid Mechanics*, 32(1), 347–382.
4. **White, F. M.** (2011). *Fluid Mechanics* (7th ed.). McGraw-Hill Education.
5. **ANSYS Inc.** (2023). *ANSYS Fluent Theory Guide, Release 2023 R2*. Canonsburg, PA.
