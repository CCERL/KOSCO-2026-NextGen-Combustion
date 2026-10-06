# 1. Lid-Driven Cavity

This tutorial introduces the basic OpenFOAM workflow using a 2D lid-driven cavity flow.

The case is simulated using the standard OpenFOAM `incompressibleFluid` module. 
The primary objective is to become familiar with the basic structure of an OpenFOAM case 
and the general workflow from case setup to solution and post-processing.

## Case description

The computational domain consists of a 2D square cavity. 
The top wall moves at a 1m/s velocity, while the remaining walls are stationary.

This configuration provides a simple example for examining the fundamental components of an OpenFOAM case
without additional complexity from thermophysical properties or chemical reactions.

## Running the case

From the tutorial directory:

```bash
cd 1.Cavity
./Allrun
```

To remove generated solution files and restore the case:

```bash
./Allclean
```

## Files to examine

The following files are particularly useful for understanding the case setup:

- `system/blockMeshDict` — computational mesh
- `system/controlDict` — simulation control
- `system/fvSchemes` — discretization schemes
- `system/fvSolution` — linear solvers and solution controls
- `0/` — initial and boundary conditions
- `constant/` — physical and model properties
