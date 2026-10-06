# 3. H₂/Air Counterflow Flame

This tutorial introduces the OpenFOAM workflow for laminar reacting-flow simulations with detailed chemistry and transport using `DTLreactingFoam`.

The primary objective is to become familiar with the simulation of laminar flames using detailed chemical kinetics and species transport models beyond the standard OpenFOAM reacting-flow framework.


## Case description

The computational domain consists of an opposed-flow configuration in which a hydrogen-containing fuel stream and an air stream enter from opposite sides of the domain.

Both inlet velocities are `0.5 m/s`, and both inlet temperatures are `300 K`. The fuel-side H₂ and N₂ mole fractions are `0.5` each, while the air-side O₂ and N₂ mole fractions are `0.21` and `0.79`, respectively. A hot internal temperature field is supplied to initialize the reacting region.

This configuration provides a simple laminar flame case for examining the coupling of detailed gas-phase chemistry and detailed species transport in `DTLreactingFoam`.

## Running the case

From the tutorial directory:

```bash
cd $FOAM_RUN/KOSCO-2026-NextGen-Combustion/Tutorial/3.CounterFlowFlame.DTM
./Allrun
```

The `Allrun` script executes the following commands sequentially:

```text
DTMchemkinToFoam
      ↓
blockMesh
      ↓
decomposePar
      ↓
mpirun
      ↓
reconstructPar
```

The script restores the DTM configuration, generates the chemistry and thermophysical data, creates the mesh, decomposes the domain, runs the simulation on four processes using `DTLreactingFoam` through `foamRun`, and reconstructs the results.

To remove the generated mesh and simulation results:

```bash
./Allclean
```

## Files to examine

The following files are particularly useful for understanding the case setup:

- `chemkin/chem.inp` — chemical mechanism, thermodynamic, and transport data
- `chemkin/therm.dat` — chemical mechanism, thermodynamic, and transport data
- `chemkin/tran.dat` — chemical mechanism, thermodynamic, and transport data
- `chemkin/transportSutherlands` — chemical mechanism, thermodynamic, and transport data
- `constant/physicalProperties` — thermophysical and detailed transport model configuration
- `constant/physicalProperties` — thermophysical and detailed transport model configuration
- `constant/physicalProperties` — thermophysical and detailed transport model configuration
- `chemkin/` — chemical mechanism, thermodynamic, and transport data
