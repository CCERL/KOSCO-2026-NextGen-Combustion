## Case description

The computational domain consists of a 2D axisymmetric wedge configuration with separate fuel, pilot, and coflow-air inlets.

This configuration provides an example for examining the structure of a turbulent reacting-flow case and the coupling of flow, species transport, chemical reactions, and combustion models in OpenFOAM.

## Running the case

From the tutorial directory:

```bash
cd $FOAM_RUN/KOSCO-2026-NextGen-Combustion/Tutorial/2.SandiaFlameD
./Allrun
```

The `Allrun` script automates the following workflow:

```text
Convert CHEMKIN chemistry and thermodynamic data
using the OpenFOAM `chemkinToFoam` utility
      ↓
Mesh generation using the OpenFOAM `blockMesh` utility
      ↓
Initialize the solution fields using the OpenFOAM `setFields` utility
      ↓
Domain decomposition using `decomposePar`
      ↓
Run the simulation in parallel using the `multicomponentFluid` module
      ↓
Reconstruct the decomposed results using `reconstructPar`
      ↓
Simulation results
```

To remove the generated mesh and simulation results:

```bash
./Allclean
```

## Files to examine

The following files and directories are particularly useful for understanding the case setup:

- `0/` — initial fields and boundary conditions
- `chemkin/` — chemical mechanism, thermodynamic, and transport data
- `constant/physicalProperties` — thermophysical and transport model configuration
- `constant/chemistryProperties` — chemistry model configuration
- `constant/combustionProperties` — combustion model configuration
- `constant/momentumTransport` — momentum transport model configuration
- `system/blockMeshDict` — computational mesh configuration
- `system/setFieldsDict` — field initialization configuration
- `system/decomposeParDict` — domain decomposition configuration
- `system/controlDict` — simulation and run-time contro
