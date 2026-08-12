# Classical Molecular Dynamics Simulation of Liquid Water

Comparative study of four classical water models (SPC, SPC/E, TIP3P, TIP4P) using GROMACS, evaluating how well each reproduces experimental structural and dynamic properties of liquid water across temperatures.

**Author:** Nitin Sharma
**Supervisor:** Prof. Arun Venkatnathan, Department of Chemistry, IISER Pune
**Project:** Summer Research Project, IISER Pune (May–July 2026)

📄 [Full report (PDF)](report/Classical_MD_Simulation_of_Liquid_Water.pdf)

![Water box snapshot](figures/fig1_water_box_snapshot.png)

## Overview

Water is deceptively hard to model accurately despite its molecular simplicity, and no single classical force field reproduces every experimental property at once. This project systematically compares four widely used rigid water models — **SPC, SPC/E, TIP3P, and TIP4P** — under the OPLS-AA force field, across four temperatures (298 K, 320 K, 340 K, 360 K), to evaluate which model best reproduces experimental density, structure, dielectric response, hydrogen bonding, and diffusion.

## Methodology

- **Software:** GROMACS 5.0.7, initial geometry optimized in Gaussian 09
- **System:** Cubic box (~8.1 nm), scaled from 500 to 10,000 water molecules to test finite-size effects; 5000 molecules used for production runs after density saturation
- **Force field:** OPLS-AA, with model-specific parameters (SPC, SPC/E, TIP3P, TIP4P)
- **Integration:** Velocity-Verlet, 1 fs timestep, 1.2 nm non-bonded cutoff
- **Equilibration:** Steepest-descent energy minimization → 10 ns NPT (Parrinello–Rahman barostat, Nosé–Hoover thermostat)
- **Production:** 25 ns NVT run per model per temperature
- **Analysis:** Radial distribution functions, coordination number, static dielectric constant (dipole moment fluctuations), hydrogen-bond statistics and lifetimes (via TRAVIS), and self-diffusion coefficients (Einstein relation on MSD)

## Key results

**Density (5000 molecules, 298 K):** all models within ~1% of the experimental value (997 kg/m³); TIP4P and SPC/E closest.

**Structure (RDFs):** SPC/E gives the closest O–H first-peak distance (0.176 nm vs. experimental 0.173 nm) and the closest coordination number (4.77 vs. experimental 4.7).

**Dielectric constant:** SPC/E performs best (70.9 vs. experimental 78.3 at 298 K); consistently decreases with increasing temperature across all models, consistent with experiment.

**Hydrogen bonding:** SPC/E shows the highest H-bonds per molecule (3.59) and longest H-bond lifetime (4.01 ps), both closest to experimental estimates (3.5–4.0 H-bonds/molecule).

**Self-diffusion:** SPC/E gives the closest self-diffusion coefficient (2.60 × 10⁻⁵ cm²/s vs. experimental 2.30 × 10⁻⁵ cm²/s).

| Property                   | Best-performing model | Experimental value |
| -------------------------- | --------------------- | ------------------ |
| Density                    | TIP4P / SPC/E         | 997 kg/m³          |
| O–H distance (RDF)         | SPC/E                 | 0.173 nm           |
| Coordination number        | SPC/E                 | 4.7                |
| Dielectric constant        | SPC/E                 | 78.3               |
| H-bonds/molecule           | SPC/E                 | 3.5–4.0            |
| Self-diffusion coefficient | SPC/E                 | 2.30 × 10⁻⁵ cm²/s  |

**Conclusion:** No single model reproduces every property exactly, but SPC/E most consistently matches experiment across structural and dynamic properties among the four models tested.

## Repository contents

- `report/` — full write-up with methodology, all RDF plots (298–360 K), MSD/diffusion plots, and hydrogen-bond autocorrelation analysis
- `figures/` — key plots extracted for quick viewing
- `data/` — density, structural/dynamic property, and H-bond lifetime tables as CSV
- `scripts/` — GROMACS `.mdp` configuration files [and analysis scripts, if included]

## Tools used

`GROMACS 5.0.7` · `Gaussian 09` · `TRAVIS` (H-bond autocorrelation) · `XMgrace` / `Python` for plotting

## Acknowledgements

This work was carried out under the supervision of Prof. Arun Venkatnathan at IISER Pune, with guidance from lab members Nayan Dey and Vishnu Sudarshan.
