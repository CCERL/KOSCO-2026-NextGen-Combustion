# 4. H₂/Air Counterflow Flame with FTM and CoTHERM

This tutorial uses the same case setup as Case 3, with the Fast Transport Model (FTM) and CoTHERM enabled in `DTLreactingFoam`.

Refer to [Case 3](../3.CounterFlowFlame.DTM/README.md) for the computational domain, inlet conditions, and general case configuration.

## Running the case

From the tutorial directory:

```bash
cd $FOAM_RUN/KOSCO-2026-NextGen-Combustion/Tutorial/4.CounterFlowFlame.FTMCO
./Allrun
```

The `Allrun` script executes the following commands sequentially:

```text
DTMchemkinToFoam
      ↓
blockMesh
      ↓
FTMchemkinToFoam
      ↓
decomposePar
      ↓
mpirun
      ↓
reconstructPar
```

Compared with Case 3, the script adds FTM preprocessing using `FTMchemkinToFoam` and enables FTM and CoTHERM before running the simulation.

## Files to examine

In addition to the files described in Case 3, examine:

- `constant/physicalProperties.PP` — baseline configuration for FTM preprocessing
- `constant/physicalProperties` — FTM and CoTHERM model configuration
- `constant/thermo.FTM` — generated species properties and preprocessed FTM transport data

