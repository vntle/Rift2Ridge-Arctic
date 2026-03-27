# Overview

## What is Rift2Ridge-Arctic?

Rift2Ridge-Arctic is a collection of model configurations, scripts, and documentation for applying the **Rift2Ridge** finite-element geodynamics code to Arctic tectonic settings. The work is based on the private research version of Rift2Ridge developed at the [MARUM Center for Marine Environmental Sciences](https://www.marum.de), University of Bremen.

## Background

### Rift2Ridge

Rift2Ridge is a 2-D finite-element code that simulates the geodynamic evolution of lithospheric rifting and mid-ocean ridge spreading. It solves the equations of conservation of mass, momentum, and energy for a visco-elasto-plastic rheology, and is capable of capturing:

- Lithospheric thinning during rifting
- Melt generation and extraction
- Crustal accretion at spreading centres
- Thermal and compositional evolution of the mantle

The core code was developed primarily by Dr. Javier García-Pintado and Prof. Dr. Marta Pérez-Gussinye at MARUM.

### Arctic Application

The Arctic Ocean contains some of the youngest and most poorly understood ocean basins on Earth, including the **Eurasia Basin** (opened ~56 Ma at the Gakkel Ridge) and the **Amerasia Basin** (origin debated). Key scientific questions addressed by this project include:

- How did ultra-slow spreading at the Gakkel Ridge evolve from continental rifting?
- What controls melt production at ultra-slow spreading rates?
- How do sediment loading and a cold mantle affect crustal architecture in Arctic basins?

## Key Features

- **Visco-elasto-plastic rheology** — captures brittle, ductile, and elastic deformation in a single framework.
- **Adaptive mesh refinement** — resolves fine-scale features (e.g., shear zones, Moho) without prohibitive computational cost.
- **Component-based model setup** — select physical components (e.g., melt, data assimilation) via the `COMPSET` mechanism in `readCASE.m`.
- **SLURM integration** — example batch scripts for HPC cluster submission are provided.
- **Arctic case studies** — pre-configured input folders for Arctic rifting scenarios.

## Repository Structure

```
Rift2Ridge-Arctic/
├── README.md              # Project overview and quick start
├── docs/                  # Documentation (this folder)
│   ├── overview.md
│   ├── installation.md
│   ├── configuration.md
│   ├── usage.md
│   ├── arctic-setup.md
│   ├── glossary.md
│   ├── faq.md
│   └── contributing.md
└── ...                    # Model input files and scripts
```

## Related Resources

- [Rift2Ridge public repository (garciapintado)](https://github.com/garciapintado/Rift2Ridge) — the upstream public code.
- [MARUM Geophysics-Geodynamics group](https://www.marum.de) — the research group behind Rift2Ridge.
- [Gakkel Ridge on Wikipedia](https://en.wikipedia.org/wiki/Gakkel_Ridge) — background reading on Arctic ultra-slow spreading.
