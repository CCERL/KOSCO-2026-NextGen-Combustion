# 2026 한국연소학회 가을 튜토리얼 Next-Gen Combustion

![OpenFOAM](https://img.shields.io/badge/OpenFOAM-12-1f6feb)
![License](https://img.shields.io/badge/license-GPL--3.0-yellow)

[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.cpc.2026.110052-red)](https://doi.org/10.1016/j.cpc.2026.110052)

## Overview
This repository provides tutorial materials for incompressible and reacting-flow simulations using OpenFOAM. The tutorials cover a basic incompressible-flow simulation using `incompressibleFluid`, a turbulent Sandia Flame D simulation using the standard OpenFOAM module `multicomponentFluid`, and a laminar counterflow-flame simulation using the custom-developed `DTLreactingFoam` framework. 

Through these cases, users can learn the basic OpenFOAM case structure, simulation setup, numerical workflow, and reacting-flow capabilities, as well as the application of `DTLreactingFoam` to detailed laminar flame simulations.

---

## Tutorial cases

| Case | Flow configuration | Solver | Key topics |
|---|---|---|---|
| [00 Cavity](Tutorial/01-cavity) | 2-D lid-driven cavity | `incompressibleFluid` | Case structure, boundary conditions, and numerical schemes |
| [01 Sandia Flame D](Tutorial/02-SandiaFlameD) | Turbulent nonpremixed flame | `multicomponentFluid` | Gas-phase chemistry, species transport, and combustion modeling |
| [02 Counterflow Flame](Tutorial/03-counterFlowFlame) | Laminar H₂/air counterflow flame | `DTLreactingFoam` | Detailed chemistry and multicomponent transport |

---

## Requirements

The tutorial cases are based on **OpenFOAM Foundation v12**.

In particular, follow the [OpenFOAM 해석 환경 구축 및 DTLreactingFoam 설치 가이드](https://github.com/CCERL/KOSCO-2026-NextGen-Combustion/blob/main/Documentation/Prerequisites/00_OpenFOAM%20해석%20환경%20구축%20및%20DTLreactingFoam%20설치%20가이드.pdf) before proceeding with the tutorial cases.

After completing the setup, verify that the OpenFOAM environment is loaded:

```bash
foamVersion
```
---

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
