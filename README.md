# 2026 한국연소학회 가을 튜토리얼 Next-Gen Combustion

![OpenFOAM](https://img.shields.io/badge/OpenFOAM-12-1f6feb)
![License](https://img.shields.io/badge/license-GPL--3.0-yellow)

[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.cpc.2026.110052-red)](https://doi.org/10.1016/j.cpc.2026.110052)

## Overview
This repository provides a tutorial package for OpenFOAM-based flow and reacting-flow simulations, designed to introduce the fundamental workflow of OpenFOAM and progressively extend it to turbulent and laminar reacting-flow applications. The tutorials cover a basic incompressible-flow simulation using `icoFoam`, a turbulent reacting-flow simulation of the Sandia Flame D using the standard OpenFOAM framework, and a laminar counterflow-flame simulation using `DTLreactingFoam`. Through these cases, users can learn the basic structure, case setup, numerical workflow, and reacting-flow simulation capabilities of OpenFOAM, together with the application of the `DTLreactingFoam` framework for detailed laminar flame simulations.

---

## Tutorial cases

| Case | Configuration | Solver / Framework | Tutorial focus |
|---|---|---|---|
| [`01-cavity`](./Tutorial/01-cavity) | Two-dimensional lid-driven cavity flow | `incompressibleFluid` | Fundamentals of OpenFOAM case structure, boundary conditions, numerical discretization, and incompressible-flow simulation |
| [`02-SandiaFlameD`](./Tutorial/02-SandiaFlameD) | Turbulent non-premixed Sandia Flame D | `multicomponentFluid` | Turbulent reacting-flow simulation with detailed gas-phase chemistry, species transport, and combustion-model setup |
| [`03-counterFlowFlame`](./Tutorial/03-counterFlowFlame) | Laminar H₂/air counterflow diffusion flame | `DTLreactingFoam` | Laminar reacting-flow simulation with detailed chemistry and detailed transport using the `DTLreactingFoam` framework |

---

## Requirements

The tutorial cases are based on **OpenFOAM Foundation v12**.

Make sure the OpenFOAM environment is loaded before running the cases:

```bash
foamVersion
```

The first two cases use solvers and models available in the standard OpenFOAM 12 environment.

> **Note**
>
> `3.counterFlowFlame` uses the custom `DTLreactingFoam` solver together with the detailed-transport models used in this tutorial.
> A standard OpenFOAM 12 installation alone is therefore not sufficient to run Case 3.
>
> Please install `DTLreactingFoam-12` before running this case:
>
> https://github.com/danhnam11/DTLreactingFoam-12

---

## Download

The recommended location is your OpenFOAM run directory:

```bash
mkdir -p $FOAM_RUN
cd $FOAM_RUN
git clone https://github.com/CCERL/KOSCO_2026_Fall_Tutorial.git
cd KOSCO_2026_Fall_Tutorial
```

To update an existing copy:

```bash
git pull
```

---

## 1. Lid-Driven Cavity

[`1.cavity`](./1.cavity) is a compact introductory case for reviewing the basic structure of an OpenFOAM simulation.

The domain is a **2-D square cavity**. The upper wall moves in the positive x-direction while the remaining walls are stationary.

The simulation is performed using standard `incompressibleFluid` module in OpenFOAM-12.

### Run

```bash
cd 1.cavity

blockMesh
foamRun
```

## 2. Sandia Flame D

[`2.SandiaFlameD`](./2.SandiaFlameD) introduces a reacting-flow calculation based on the well-known **Sandia Flame D** configuration.

The case uses an axisymmetric wedge mesh with separate methane-fuel, pilot, and coflow-air inlets.

The simulation is performed using standard `multicomponentFluid` module in OpenFOAM-12.

### Run

```bash
cd 2.SandiaFlameD

blockMesh
setFields
foamRun
```

For parallel execution, use the supplied decomposition settings:

```bash
cd 2.SandiaFlameD

blockMesh
setFields
decomposePar
mpirun -np 4 foamRun -parallel
reconstructPar
rm -r processor*
```

## 3. H₂/Air Counterflow Flame

[`3.counterFlowFlame`](./3.counterFlowFlame) is an opposed-flow reacting case in which a hydrogen-containing fuel stream and an air stream enter from opposite sides of the domain.

The supplied inlet velocities are:
```text
fuel : 0.5 m/s
air  : 0.5 m/s
```
Both inlet temperatures are initialized at `300 K`. A hot internal field is supplied to initialize the reacting region.

The fuel-side hydrogen mass fraction is:
```text
Y_H2 = 0.0673
```

while the air-side oxygen mass fraction is:
```text
Y_O2 = 0.23
```

The simulation is performed using custom `DTLreactingFoam` solver.

### Run

```bash
cd 3.counterFlowFlame

blockMesh
foamRun
```

Parallel execution can be performed in the same way:

```bash
cd 3.counterFlowFlame

blockMesh
decomposePar
mpirun -np 4 foamRun -parallel
reconstructPar
rm -r processor*
```

---

## Notes for the tutorial

These cases are intentionally compact so that the important OpenFOAM settings can be inspected directly.

Rather than treating the case files as black boxes, participants are encouraged to compare:

- mesh and boundary-condition definitions,
- incompressible and reacting-flow solver structures,
- thermophysical and chemistry models,
- numerical schemes and timestep settings,
- serial and MPI execution workflows.

The three cases are intended to provide a gradual path from a basic OpenFOAM CFD calculation to detailed reacting-flow simulations.
