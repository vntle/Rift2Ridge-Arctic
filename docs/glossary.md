# Glossary

A reference of geodynamics terminology and code-specific terms used in Rift2Ridge-Arctic.

---

## A

**Adaptive mesh refinement (AMR)**
A numerical technique that dynamically increases mesh resolution in regions of interest (e.g., near faults or the Moho) while using coarser elements elsewhere to reduce computational cost.

**Amagmatic spreading**
Seafloor spreading in which lithospheric extension occurs entirely by brittle faulting with no magmatic accretion. Observed in some segments of the Gakkel Ridge.

**Asthenosphere**
The rheologically weak upper part of the mantle, below the lithosphere, where convective flow occurs. Typically begins at depths of 50–200 km.

---

## B

**Brittle–ductile transition (BDT)**
The depth (or temperature) at which deformation mode switches from brittle (frictional) failure to ductile (viscous/plastic) flow. In the crust, typically around 300–400 °C for quartz-rich rocks.

---

## C

**COMPSET**
Component set. A MATLAB structure defined in `readCASE.m` that activates or deactivates physical sub-models (e.g., melt generation, data assimilation, Monte-Carlo sampling).

**Cohesion (C)**
The yield strength of a rock at zero confining pressure, in the Mohr–Coulomb failure criterion: `τ = C + σ_n tan(φ)`.

**Continental rifting**
The process of lithospheric extension that thins and eventually ruptures continental crust, potentially leading to the formation of a new ocean basin.

**Crustal accretion**
The addition of new igneous material to the crust at a spreading centre, forming new oceanic crust from mantle-derived melt.

---

## D

**Detachment fault**
A low-angle, long-lived normal fault that accommodates significant lithospheric extension and can exhume lower-crustal or mantle rocks at the seafloor (oceanic core complexes).

**Dry solidus**
The melting curve of mantle peridotite in the absence of water. The presence of water lowers the solidus temperature significantly.

---

## E

**Eurasia Basin**
One of the two main deep-water basins of the Arctic Ocean, opened since ~56 Ma as the Gakkel Ridge propagated northward.

---

## F

**Finite-element method (FEM)**
A numerical technique for solving partial differential equations by discretising the domain into elements and approximating the solution with polynomial basis functions. Rift2Ridge uses FEM for its momentum and energy solvers.

---

## G

**Gakkel Ridge**
An ultra-slow spreading mid-ocean ridge located in the Eurasia Basin of the Arctic Ocean. With half-rates of 6–13 mm/yr, it is the slowest spreading centre on Earth.

**GIA (Glacial Isostatic Adjustment)**
The response of the solid Earth to changes in ice-sheet loading. Relevant in the Arctic due to repeated glaciations during the Pleistocene.

---

## H

**Half-spreading rate**
The velocity of one plate relative to the ridge axis. Total spreading rate = 2 × half-spreading rate.

**Harzburgite**
A peridotite depleted of basaltic components by previous melt extraction. Forms the residual mantle beneath the oceanic crust.

---

## L

**Lithosphere**
The rigid outer shell of the Earth comprising the crust and uppermost mantle. Its thickness is controlled by temperature (the ~1300 °C isotherm marks its base).

**Lomonosov Ridge**
An underwater ridge that bisects the Arctic Ocean. It rifted from the Siberian/Eurasian continental margin ~56 Ma during Eurasia Basin opening.

---

## M

**Mantle potential temperature (T_p)**
The temperature that mantle material would have if brought adiabatically to the surface without melting. A standard reference for comparing thermal states of different mantle regions. Typical MORB mantle: ~1300 °C.

**MARUM**
Center for Marine Environmental Sciences, University of Bremen. The institution where the core Rift2Ridge code was developed.

**Moho (Mohorovičić discontinuity)**
The boundary between the crust and the mantle, marked by an increase in seismic velocity. Typical depth: ~7 km beneath oceans, ~35 km beneath continents.

**Monte-Carlo sampling**
A statistical method that samples model parameters from prescribed distributions to quantify uncertainty in model outputs. Activated by `COMPSET.mc = true`.

---

## O

**Oceanic core complex (OCC)**
A dome-shaped seafloor feature formed by long-lived detachment faulting that exhumes deep crustal or mantle rocks. Common at slow and ultra-slow spreading ridges.

---

## P

**Peridotite**
A coarse-grained, olivine-rich rock that makes up most of the Earth's upper mantle.

**Plastic yielding**
The onset of irreversible deformation when stress exceeds the yield strength (cohesion + friction). Represented by the Mohr–Coulomb criterion in Rift2Ridge.

---

## R

**Rheology**
The study of deformation and flow of materials. Rift2Ridge uses a **visco-elasto-plastic** rheology, combining viscous creep, elastic deformation, and plastic failure.

---

## S

**Solidus**
The temperature below which a rock is completely solid. Above the solidus, partial melting begins.

**SuiteSparse**
An open-source library of sparse matrix algorithms. Rift2Ridge uses it for efficient solution of large linear systems.

**SLURM**
Simple Linux Utility for Resource Management — a workload manager used on many HPC clusters to schedule and manage batch jobs.

---

## T

**Triangle**
A 2-D quality mesh generation program used by Rift2Ridge to create unstructured triangular meshes.

---

## U

**Ultra-slow spreading**
Spreading rates below ~20 mm/yr (full rate). Characterised by intermittent magmatism, thick lithosphere, and exposure of mantle peridotite at the seafloor.

---

## V

**Visco-elasto-plastic (VEP) rheology**
A composite rheological model in which a material can simultaneously behave as a viscous fluid (creep), an elastic solid (reversible deformation), and a plastic body (irreversible failure when yield stress is exceeded).

**Viscosity (η)**
The resistance of a material to flow. In Rift2Ridge, viscosity depends on temperature, pressure, strain rate, and composition, and is bounded by `eta_min` and `eta_max`.
