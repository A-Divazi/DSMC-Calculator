# DSMC-Calculator

A graphical engineering calculator for the **preliminary design and numerical setup** of Direct Simulation Monte Carlo (DSMC) simulations of rarefied / hypersonic gas flows.

<img width="825" height="520" alt="DSMC-Calculator interface" src="https://github.com/user-attachments/assets/7831f46b-dc63-4ec4-9263-e63254c3f335" />

It bridges the **macroscopic** flow conditions (pressure, temperature, velocity, Mach/Re) with the **molecular and numerical** scales required to build a DSMC case (mean free path, cell size, time step, particle statistical weight). It is a *setup / pre-simulation aid* — it suggests consistent DSMC grid and time parameters, it does not run the DSMC simulation itself.

> **License:** MIT (see [`LICENSE`](LICENSE)).
> **If you use this in research, please cite it** (a `CITATION.cff` is included,
> so GitHub shows a "Cite this repository" button):
> > A. Divazi, *DSMC-Calculator: a graphical calculator for DSMC and rarefied
> > gas dynamics*, 2026. https://github.com/A-Divazi/DSMC-Calculator

## Features

**Thermodynamics**
- Pressure, number density, mass density, speed of sound, specific gas constant.

**VHS molecular model**
- Collision cross-section, mean free path, mean thermal speed, mean collision time, dynamic viscosity.

**Dimensionless flow parameters**
- Knudsen number (rarefaction regime), Reynolds number, Mach number.

**Inverse design**
- Target `Kn` → required number density `n` and pressure `P`.
- Target `Re` → required velocity `U` and Mach `M`.

**DSMC discretization guidance**
- Suggested cell volume and cell dimension `Δx`, real molecules per cell, particle statistical weight `nEquivalentParticles` (`Neq`).
- Two-way particle weighting (`Nppc` ⇄ `nEquivalentParticles`).

**Time-step guidance**
- Collision-limited and transit-limited time steps, with user-adjustable safety factors.

**Boundary-layer estimates**
- Recovery temperature, Eckert reference temperature, flat-plate boundary-layer thicknesses (`δ`, `θ`, `δ*`).

The GUI has an interactive results panel and a formulas/equations panel, with hint icons next to each input.

## Getting started

You can run it from source, or use a prebuilt executable.

### Run from source (needs Python 3 + Tkinter)

```bash
python3 dsmc_calc.py
```

- Linux: `sudo apt install python3-tk` if Tkinter is missing.
- Windows/macOS: any Python 3 install that ships Tkinter (python.org builds do).

### Prebuilt executables

Prebuilt apps are in [`releases/`](releases/):

- `DSMC_Calculator_Linux` — Linux (built with PyInstaller; run `./DSMC_Calculator_Linux`).
- `DSMC_Calculator_Windows.exe` — Windows.

See [`BUILDING.md`](BUILDING.md) to rebuild from source on either platform.

## Usage

Enter the macroscopic state (e.g. temperature, pressure/velocity, and a characteristic length) and the gas parameters (molecular mass, reference diameter, VHS viscosity index `ω`, specific-heat ratio, Prandtl number). The tool then reports molecular properties, dimensionless numbers, and the recommended DSMC grid / time-step / particle-weight settings, and lets you run the inverse (`Kn`, `Re`) and particle-weight conversions.

## Documentation

The full mathematical and physical formulation (all equations, assumptions, and unit conventions) is in:

[`docs/DSMC_Calculator_Mathematical_Documentation.pdf`](docs/DSMC_Calculator_Mathematical_Documentation.pdf)

## Repository layout

```
dsmc_calc.py                      # the application (single-file Tkinter GUI)
docs/                             # mathematical / physical documentation (PDF)
releases/                         # prebuilt executables (Linux, Windows)
DSMC_Calculator.spec              # PyInstaller spec used to build the executables
BUILDING.md                       # how to build/package from source
```

## Notes & scope

- This is a **preliminary-design / sanity-check** tool. It gives physically consistent DSMC setup parameters from macroscopic inputs; it does **not** verify DSMC statistical convergence, cell-size-vs-mean-free-path validity of an actual mesh, or solver results.
- Always check units and the underlying assumptions in the documentation PDF before relying on the numbers for a full simulation.
