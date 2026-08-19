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
| 0°              | ~0 | 0.00252155 |
| 4°              | ~0 | 0.00252155 |
| 15°             | ~0 | 0.00252156 |

**Key observations:**
- **Cd is physically consistent** (~0.00252) and positive, confirming the force calculation is working.
- **Cl ≈ 0 for all angles** — the mesh still does not resolve the boundary layer for SST, despite ideal y+.
- **y+ validation:** `min = 1.6e-06, max = 0.0011, average = 0.00035` — ideal for SST.
- **Next step:** Increase `zCells` (120 → 250) and `zGrading` (100k → 1M) to capture the boundary layer and obtain realistic Cl.
## Modifications Made

- Added `0/rho` field for force coefficient calculation.
- Added `forceCoeffs` function object to `system/controlDict`.
- Modified `0/U` for different angles of attack.
- Switched turbulence model to `kOmegaSST`.
- Created a custom mesh via `blockMesh` with a common `blockMeshDict` linked from all cases.
