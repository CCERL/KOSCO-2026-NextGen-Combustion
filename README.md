# 2026 한국연소학회 가을 튜토리얼 Next-Gen Combustion

![OpenFOAM](https://img.shields.io/badge/OpenFOAM-12-1f6feb)
![License](https://img.shields.io/badge/license-GPL--3.0-yellow)

[![DOI](https://img.shields.io/badge/DOI-10.1016%2Fj.cpc.2026.110052-red)](https://doi.org/10.1016/j.cpc.2026.110052)

## Overview
This repository provides tutorial materials for incompressible and reacting-flow simulations using OpenFOAM. The tutorials cover a basic incompressible-flow simulation using `incompressibleFluid`, a turbulent Sandia Flame D simulation using the standard OpenFOAM module `multicomponentFluid`, and a laminar counterflow-flame simulation using the custom-developed `DTLreactingFoam` framework. 

Through these cases, users can learn the basic OpenFOAM case structure, simulation setup, numerical workflow, and reacting-flow capabilities, as well as the application of `DTLreactingFoam` to detailed laminar flame simulations.

---

## Tutorial Cases

### 1. [Lid-Driven Cavity](Tutorial/1.Cavity)

A basic incompressible-flow case using `incompressibleFluid`, introducing the OpenFOAM case structure, numerical setup, and execution workflow.

### 2. [Sandia Flame D](Tutorial/2.SandiaFlameD)

A turbulent reacting-flow case using `multicomponentFluid`, introducing chemical kinetics, thermophysical properties, and combustion modeling.

### 3. [H₂/Air Counterflow Flame](Tutorial/3.CounterFlowFlame.DTM)

A laminar opposed-flow flame using `DTLreactingFoam`, introducing detailed chemistry and species transport.

### 4. [FTM and CoTHERM](Tutorial/4.CounterFlowFlame.FTMCO)

An extension of Case 3 using the same flame configuration, introducing FTM preprocessing and the use of FTM and CoTHERM in `DTLreactingFoam`.


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

---

## Download

Clone the tutorial repository into your OpenFOAM run directory:

```bash
# Create the OpenFOAM run directory if it does not exist
mkdir -p "$FOAM_RUN"

# Move to the OpenFOAM run directory
cd "$FOAM_RUN"

# Download the tutorial repository
git clone https://github.com/CCERL/KOSCO-2026-NextGen-Combustion.git

# Move to the downloaded repository
cd KOSCO-2026-NextGen-Combustion
```

`$FOAM_RUN` is the user run directory defined by the OpenFOAM environment.

---
