# 2. Sandia Flame D

This tutorial introduces the OpenFOAM workflow for turbulent reacting-flow simulations using the Sandia Flame D configuration.

The case is simulated using the standard OpenFOAM `multicomponentFluid` module. The primary objective is to become familiar with the additional case setup required for reacting-flow simulations, including thermophysical properties, chemical kinetics, species transport, and combustion modeling.

## Case description

The computational domain consists of a 2D axisymmetric wedge configuration with separate fuel, pilot, and coflow-air inlets.

This configuration provides an example for examining the structure of a turbulent reacting-flow case and the coupling of flow, species transport, chemical reactions, and combustion models in OpenFOAM.

## Running the case

From the tutorial directory:

```bash
cd $FOAM_RUN/KOSCO-2026-NextGen-Combustion/Tutorial/2.SandiaFlameD
./Allrun
```

The `Allrun` script executes the following commands sequentially:

```text
chemkinToFoam
      ↓
blockMesh
      ↓
setFields
      ↓
decomposePar
      ↓
mpirun
      ↓
reconstructPar
```

The script converts the CHEMKIN mechanism into the OpenFOAM format, generates the computational mesh, initializes the solution fields, decomposes the domain, runs the simulation in parallel using the `multicomponentFluid` module, and reconstructs the decomposed results.

To remove the generated mesh and simulation results:

```bash
./Allclean
```

## Files to examine

The following files and directories are particularly useful for understanding the case setup:

- `0/` — initial fields and boundary conditions
- `chemkin/chem.inp` — chemical species and reaction mechanism
- `chemkin/therm.dat` — species thermodynamic data
- `chemkin/transportSutherlands` — species transport data for the Sutherland model
- `constant/physicalProperties` — thermophysical and transport model configuration
- `constant/chemistryProperties` — chemistry model configuration
- `constant/combustionProperties` — combustion model configuration
- `constant/momentumTransport` — momentum transport model configuration
- `system/blockMeshDict` — computational mesh configuration
- `system/setFieldsDict` — field initialization configuration
- `system/decomposeParDict` — domain decomposition configuration
