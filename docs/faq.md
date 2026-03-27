# FAQ

Frequently asked questions about Rift2Ridge-Arctic.

---

## General

### What is Rift2Ridge-Arctic?

Rift2Ridge-Arctic adapts the Rift2Ridge finite-element geodynamics code (developed at MARUM, University of Bremen) to Arctic tectonic settings. It provides model configurations, scripts, and documentation for simulating rifting and ultra-slow spreading in the Arctic Ocean. See the [Overview](overview.md) for more detail.

### Is the full Rift2Ridge source code available here?

No. The core Rift2Ridge solver is a private research code. This repository contains Arctic-specific input configurations, post-processing scripts, and documentation. The public upstream repository is at [garciapintado/Rift2Ridge](https://github.com/garciapintado/Rift2Ridge).

### What MATLAB version is required?

MATLAB R2018b or later is recommended. Some MATLAB Toolboxes may be required depending on the COMPSET components enabled (e.g., the Optimization Toolbox for data assimilation).

### Can I run the model on Windows?

Yes, though Rift2Ridge is primarily tested on Linux and macOS. Running on Windows may require substantial modifications to shell scripts and path handling.

---

## Installation

### I get "triangle: command not found". How do I fix it?

Ensure the `triangle` binary is compiled and its directory is on your `PATH`:

```bash
export TRIANGLE_PATH=$HOME/Library/MatlabLib/triangle
export PATH=$PATH:$TRIANGLE_PATH
```

Then reload your shell: `source ~/.bash_profile`.

### MATLAB cannot find the `mutils` functions.

If you copied the `mutils` folder from another researcher's computer, the `.mexw64` binaries will not match your CPU/MATLAB version.

* 📂 **Step 1:** Navigate to the `mutils/MATLAB` directory in your MATLAB Current Folder.

* ⚙️ **Step 2:** Type `mutils_setup` in the Command Window to recompile the C-code specifically for your machine using the MinGW compiler.

* 🔗 **Step 3:** Ensure the folder is permanently added to your path: `addpath(genpath(getenv('MUTILS_PATH'))); savepath;`.
Check that `MUTILS_PATH` is set and that `mutils` has been compiled and added to MATLAB's path. Inside MATLAB, run:

```matlab
addpath(genpath(getenv('MUTILS_PATH')));
```

Or add this line to your `startup.m` file so it runs automatically at MATLAB startup.

### What is the minimum RAM required?

A typical Arctic simulation at 500 m mesh resolution requires approximately 8–16 GB of RAM. Finer meshes or longer domains may require 32–64 GB. Use the `dx_min` parameter to adjust mesh resolution and memory usage.

---

## Running Simulations

### How do I check if my simulation is running correctly?

Monitor the log file:

```bash
tail -f rift2ridge.log
```

A healthy run prints time-step information with increasing model time. If MATLAB prints repeated warnings or the time step drops to very small values, check for numerical instability (see Troubleshooting in the [Usage](usage.md) guide).

### The simulation diverges (NaN values). What can I do?

Common causes and fixes:

1. **Time step too large** — add `p.dt = 1e10;` (in seconds) to `change_model.m` to set a smaller initial time step.
2. **Viscosity too low** — increase `p.eta_min` (e.g., from 1e18 to 5e18 Pa·s).
3. **Mesh too coarse in a high-strain zone** — decrease `dx_min` near the ridge axis.
4. **Temperature boundary condition** — ensure surface and basal temperatures are physically reasonable.

### Can I run multiple cases in parallel?

Yes. Each case lives in its own `nnn` folder and writes output to a separate directory under `$WORK`. You can submit multiple SLURM jobs simultaneously, one per case. Ensure that each job has sufficient memory and CPU resources.

### How do I continue a stopped run?

If there is an error that stop you from running, you can uncomment the line in  `call_main.m` to make it continue with the output file.
Copy the input folder to a new `nnn` subdirectory, then edit `update_model.m` to specify the restart `.mat` file and update any paths for the new machine or queue. Launch from the new folder.

---

## Arctic Science

### Why is the Gakkel Ridge special?

The Gakkel Ridge is the slowest-spreading mid-ocean ridge on Earth (full rate: ~13–26 mm/yr). At such low spreading rates, the mantle cools more efficiently, so less melt is produced. Some segments are entirely amagmatic — the crust is formed by brittle faulting and mantle exhumation with no volcanic activity. This makes the Gakkel Ridge an extreme end-member for testing geodynamic models.

### Does the model include ice loading or GIA?

Not in the current version. Glacial isostatic adjustment (GIA) due to Pleistocene ice sheets is not yet implemented. This is a planned future addition. For now, long-term tectonic simulations (Cenozoic timescales) are unaffected, but Quaternary subsidence analyses should account for GIA separately.

### What data can I use to validate Arctic simulations?

Key observational datasets for the Arctic include:

- **Bathymetry**: IBCAO (International Bathymetric Chart of the Arctic Ocean)
- **Seismic refraction/reflection**: Published crustal thickness profiles from Gakkel Ridge and Lomonosov Ridge expeditions
- **Heat flow**: Arctic heat flow database (IHFC)
- **Gravity anomalies**: Arctic free-air and Bouguer anomaly grids (e.g., from EIGEN or ArcGP)
- **Magnetic anomalies**: Seafloor spreading anomalies used for age-depth models

---

## Contributing

### How can I report a bug or suggest an improvement?

Please open a [GitHub Issue](https://github.com/vntle/Rift2Ridge-Arctic/issues) with a clear description of the problem or suggestion. Include the relevant simulation case, MATLAB version, and any error messages.

### Can I contribute a new Arctic case study?

Yes! See the [Contributing](contributing.md) guide for instructions on adding new case study folders and documentation.
