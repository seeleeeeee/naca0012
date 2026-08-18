# NACA 0012 Parametric Study (OpenFOAM)

**Objective:**  
Parametric aerodynamic study of the NACA 0012 airfoil at multiple angles of attack using OpenFOAM (steady-state, incompressible, turbulent flow).

## Setup

| Parameter | Value |
|-----------|-------|
| **Solver** | `foamRun` (incompressibleFluid) |
| **Turbulence model** | k-omega SST |
| **Velocity** | 40 m/s |
| **Reynolds number** | ~ 4 × 10⁵ |
| **Mesh size** | 16,200 cells (coarse, for initial validation) |

## Results (Current Mesh)

| Angle of Attack | Cl | Cd |
|-----------------|----|----|
| 0°              | ~0 | 0.00235 |
| 4°              | ~0 | 0.00235 |
| 15°             | ~0 | 0.00234 |

**Key observations:**
- **Cd is physically consistent** (~0.00235) and positive, confirming the force calculation is working.
- **Cl ≈ 0 for all angles** due to the coarse mesh (y+ ≈ 18). The current grid does not resolve the boundary layer for the SST model.
- **Next step:** Refine the mesh to achieve y+ ≈ 1 and obtain realistic Cl values.

## Modifications Made

- Added `0/rho` field for force coefficient calculation.
- Added `forceCoeffs` function object to `system/controlDict`.
- Modified `0/U` for different angles of attack.
- Switched turbulence model to `kOmegaSST`.
- Created a custom mesh via `blockMesh` with a common `blockMeshDict` linked from all cases.
