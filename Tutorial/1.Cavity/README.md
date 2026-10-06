# 1. Lid-Driven Cavity

This tutorial introduces the basic OpenFOAM workflow using a 2D lid-driven cavity flow.

The case is simulated using the standard OpenFOAM `incompressibleFluid` module. The primary objective is to become familiar with the basic structure of an OpenFOAM case and the general workflow from case setup to solution and post-processing.

## Case description

The computational domain consists of a 2D square cavity. The top wall moves at a velocity of `1 m/s`, while the remaining walls are stationary.

This configuration provides a simple example for examining the fundamental components of an OpenFOAM case without additional complexity from thermophysical properties or chemical reactions.

## Running the case

From the tutorial directory:

```bash
cd $FOAM_RUN/KOSCO-2026-NextGen-Combustion/Tutorial/1.Cavity
./Allrun
```

The `Allrun` script executes the following commands sequentially:

```text
blockMesh
      ↓
foamRun
```

The script generates the computational mesh and runs the simulation using the `incompressibleFluid` module.

To remove the generated mesh and simulation results:

```bash
./Allclean
```

## Files to examine

The following files are particularly useful for understanding the case setup:

- `0/p` — pressure field and boundary conditions
- `0/U` — velocity field and boundary conditions
- `constant/momentumTransport` — momentum transport model configuration
- `constant/physicalProperties` — fluid physical properties
- `system/blockMeshDict` — computational mesh configuration
- `system/controlDict` — simulation and run-time control
