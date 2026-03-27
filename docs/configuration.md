# Configuration

This page describes the configuration files and key parameters used in Rift2Ridge-Arctic simulations.

## Input Folder Structure

Each simulation lives in a dedicated input folder. The folder tree follows the convention:

```
$dsnmod/data/<region>/<event>/<meshnam>/<nnn>/
```

| Variable | Example | Description |
|---|---|---|
| `region` | `MAR`, `ARCTIC` | Tectonic region |
| `event` | `sp2`, `gakkel01` | Named simulation event |
| `meshnam` | `ucr1000` | Mesh identifier |
| `nnn` | `001` | Run number (for ensembles) |

where `$dsnmod` is typically the `SIU3P` folder in the repository.

## Configuration Files

Each input folder contains the following MATLAB scripts, which override model defaults:

### `call_main.m`

Defines the input folder tree and calls `main.m`. This is the entry point for every simulation.

```matlab
% Example call_main.m
region  = 'ARCTIC';
event   = 'gakkel01';
meshnam = 'ucr500';
nnn     = '001';
main
```

### `readCASE.m`

Defines the physical components included in the simulation (the **COMPSET**). Each component activates a block of parameters in `param_defaults()`.

```matlab
% Example readCASE.m
COMPSET.melt    = true;   % include melt generation
COMPSET.da      = false;  % data assimilation (not publicly available)
COMPSET.mc      = false;  % Monte-Carlo sampling
```

### `change_model.m`

Overrides default parameter values at initialisation. This is the main file for tuning physical parameters.

```matlab
% Example change_model.m
p.eta_min  = 1e18;   % minimum viscosity [Pa s]
p.eta_max  = 1e25;   % maximum viscosity [Pa s]
p.T_mantle = 1300;   % potential mantle temperature [°C]
```

### `update_model.m`

Applied when **continuing** a run on a different computer or **branching** from an existing run. Use this to update paths or restart parameters without modifying `change_model.m`.

### `readCF.m`

Data-assimilation options. Required even when DA is disabled (can be an empty file).

### `readMC.m`

Monte-Carlo sampling parameters. Required when `COMPSET.mc = true`.

## Key Parameters

The following parameters (set in `change_model.m` or `param_defaults.m`) are the most commonly tuned for Arctic simulations:

### Thermal Parameters

| Parameter | Default | Unit | Description |
|---|---|---|---|
| `T_mantle` | 1300 | °C | Mantle potential temperature |
| `T_surface` | 0 | °C | Surface temperature |
| `kappa` | 1e-6 | m²/s | Thermal diffusivity |
| `Cp` | 1200 | J/(kg·K) | Heat capacity |

### Rheological Parameters

| Parameter | Default | Unit | Description |
|---|---|---|---|
| `eta_min` | 1e18 | Pa·s | Minimum viscosity |
| `eta_max` | 1e25 | Pa·s | Maximum viscosity |
| `C_crust` | 20 | MPa | Crustal cohesion |
| `phi_crust` | 30 | ° | Crustal internal friction angle |

### Spreading Parameters

| Parameter | Default | Unit | Description |
|---|---|---|---|
| `v_spread` | — | mm/yr | Half-spreading rate |
| `t_end` | — | Myr | Total simulation time |
| `dt_out` | — | Myr | Output interval |

### Mesh Parameters

| Parameter | Default | Unit | Description |
|---|---|---|---|
| `nx` | — | — | Number of horizontal nodes |
| `nz` | — | — | Number of vertical nodes |
| `dx_min` | — | km | Minimum element size |

## Output

Model output is written to `$WORK/<region>/<event>/<meshnam>/<nnn>/`. Output files are MATLAB `.mat` binary files, one per output time step. See the [Usage](usage.md) guide for how to load and visualise the output.
