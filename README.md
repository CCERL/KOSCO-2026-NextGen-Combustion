# 2026 한국연소학회 가을 튜토리얼 Next-Gen Combustion

![OpenFOAM](https://img.shields.io/badge/OpenFOAM-12-1f6feb)
![License](https://img.shields.io/badge/license-GPL--3.0-yellow)

[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.cpc.2026.110052-red)](https://doi.org/10.1016/j.cpc.2026.110052)

## Overview
This repository provides tutorial materials for incompressible and reacting-flow simulations using OpenFOAM. The tutorials cover a basic incompressible-flow simulation using `incompressibleFluid`, a turbulent Sandia Flame D simulation using the standard OpenFOAM module `multicomponentFluid`, and a laminar counterflow-flame simulation using the custom-developed `DTLreactingFoam` framework. 

Through these cases, users can learn the basic OpenFOAM case structure, simulation setup, numerical workflow, and reacting-flow capabilities, as well as the application of `DTLreactingFoam` to detailed laminar flame simulations.

---

## Tutorial Cases

| Case | Configuration | Solver | Key topics |
|---|---|---|---|
| [1.Cavity](Tutorial/1.Cavity) | 2-D cavity | `incompressibleFluid` | Case setup and numerics |
| [2.SandiaFlameD](Tutorial/2.SandiaFlameD) | Turbulent flame | `multicomponentFluid` | Chemistry and combustion |
| [3.CounterFlowFlame](Tutorial/3.CounterFlowFlame) | Laminar H₂/air flame | `DTLreactingFoam` | Detailed transport |

Refer to each case README for the case description, execution workflow, and files to examine.

## Requirements

These tutorials require OpenFOAM Foundation v12 in a Linux environment. Windows users must first install **Windows Subsystem for Linux (WSL)** and set up OpenFOAM within WSL.

Cases 3 and 4 additionally require [`DTLreactingFoam-12`](https://github.com/danhnam11/DTLreactingFoam-12).

Follow the [installation guide](https://github.com/CCERL/KOSCO-2026-NextGen-Combustion/blob/main/Documentation/Prerequisites/1.OpenFOAM%20해석%20환경%20구축%20및%20DTLreactingFoam%20설치%20가이드.pdf) to set up WSL, install OpenFOAM 12, and build `DTLreactingFoam-12` before starting the tutorials.

Verify that the OpenFOAM environment is loaded:

```bash
foamVersion
```

The command should report OpenFOAM-12.

## Requirements

These tutorials are developed for **OpenFOAM Foundation v12** and must be run in a Linux environment.

Windows users must first install **Windows Subsystem for Linux (WSL)**. OpenFOAM Foundation v12 and the [`DTLreactingFoam-12`](https://github.com/danhnam11/DTLreactingFoam-12) framework should then be installed within the WSL environment. `DTLreactingFoam-12` is required to perform laminar reacting-flow simulations with detailed chemistry and multicomponent transport.

Detailed instructions for setting up WSL, installing OpenFOAM 12, and building `DTLreactingFoam-12` are provided in the [OpenFOAM 해석 환경 구축 및 DTLreactingFoam 설치 가이드](https://github.com/CCERL/KOSCO-2026-NextGen-Combustion/blob/main/Documentation/Prerequisites/1.OpenFOAM%20해석%20환경%20구축%20및%20DTLreactingFoam%20설치%20가이드.pdf). Complete the setup described in this guide before starting the tutorials.

After completing the installation, open a WSL terminal and verify that the OpenFOAM environment is loaded:

```bash
foamVersion
```

The command should report **OpenFOAM-12**.

---

## Download

The recommended location is your OpenFOAM run directory:

```bash
mkdir -p $FOAM_RUN
cd $FOAM_RUN
git clone https://github.com/CCERL/KOSCO-2026-NextGen-Combustion.git
cd KOSCO-2026-NextGen-Combustion
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
