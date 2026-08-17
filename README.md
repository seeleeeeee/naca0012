# NACA 0012 Parametric Study (OpenFOAM)

**Objective:**  
Compare aerodynamic performance of NACA 0012 airfoil at 0° and 15° angles of attack using OpenFOAM (steady-state, incompressible, turbulent flow).

## Setup
- **Solver:** `foamRun` (incompressibleFluid)
- **Turbulence:** LaunderSharmaKE (RAS)
- **Velocity:** 40 m/s
- **Reynolds number:** ~ 4 × 10⁵

## Modifications to Standard Tutorial
- Added `0/rho` field for force coefficient calculation.
- Added `forceCoeffs` function object to `system/controlDict`.
- Modified `0/U` for different angles of attack.

## Results

**Turbulence model:** k-omega SST (used for all cases)

| Angle of Attack | Cl      | Cd      |
|-----------------|---------|---------|
| 0°              | 1.034   | -0.034  |
| 4°              | 0.996   | -0.041  |
| 15°             | 2.516   | -0.529  |

**Note:** Negative Cd values indicate a coordinate system convention issue (drag direction is opposite to the flow). The magnitude of Cd is what matters for comparison.

**Takeaway:**  
As the angle of attack increases, both lift (Cl) and drag (Cd) increase. However, the Cd growth outpaces Cl growth, confirming the fundamental aerodynamic trade-off: more downforce comes at a cost in drag.
