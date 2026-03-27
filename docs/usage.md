# Usage

This page explains how to run Rift2Ridge-Arctic simulations and work with the model output.

## Running a Simulation

### Interactive Mode

1. Open a terminal, navigate to the input folder, and launch MATLAB:

   ```bash
   cd $dsnmod/data/ARCTIC/gakkel01/ucr500/001
   matlab &
   ```

2. Inside MATLAB, run:

   ```matlab
   pid = 0;
   call_main
   ```

### Batch Mode (Recommended)

For unattended runs, use MATLAB's batch mode from the terminal:

```bash
cd $dsnmod/data/ARCTIC/gakkel01/ucr500/001
matlab -nosplash -nodisplay -batch "pid=0;call_main" -logfile rift2ridge.log
```

The log file `rift2ridge.log` captures all MATLAB output and is useful for diagnosing errors.

### SLURM Cluster

An example SLURM submission script is provided in `scripts/`. Adapt it for your cluster:

```bash
#!/bin/bash
#SBATCH --job-name=r2r_arctic
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --time=48:00:00
#SBATCH --partition=compute

module load matlab/R2022b

cd $dsnmod/data/ARCTIC/gakkel01/ucr500/001
matlab -nosplash -nodisplay -batch "pid=0;call_main" -logfile rift2ridge.log
```

Submit with:

```bash
sbatch run_rift2ridge.sh
```

## Monitoring Progress

During a run, Rift2Ridge prints time-step information to the log file. You can follow the log in real time:

```bash
tail -f rift2ridge.log
```

Output `.mat` files are written to `$WORK/<region>/<event>/<meshnam>/<nnn>/` at the interval specified by `dt_out`.

## Loading Output in MATLAB

```matlab
% Load a specific time step
outdir = fullfile(getenv('WORK'), 'ARCTIC', 'gakkel01', 'ucr500', '001');
files  = dir(fullfile(outdir, '*.mat'));
S      = load(fullfile(outdir, files(end).name));  % load last step

% Basic fields
figure;
pcolor(S.X, S.Z, S.T);   % temperature field
shading interp;
colorbar;
title('Temperature [°C]');
```

## Post-processing Scripts

Python scripts for post-processing are located in the `scripts/` directory:

| Script | Description |
|---|---|
| `scripts/plot_cross_section.py` | Plot lithospheric cross sections |
| `scripts/extract_moho.py` | Extract Moho depth from output |
| `scripts/make_animation.py` | Create time-lapse animations |

Run a script with:

```bash
python3 scripts/plot_cross_section.py --outdir $WORK/ARCTIC/gakkel01/ucr500/001
```

## Restarting / Branching a Run

To continue a run from a saved state (e.g., after a cluster time limit or to test a parameter change):

1. Copy the input folder to a new `nnn` directory (e.g., `002`).
2. Edit `update_model.m` to set the restart file path and any changed parameters.
3. Launch the new run from the new `nnn` directory.

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| `triangle: command not found` | `$TRIANGLE_PATH` not on `PATH` | Check `export PATH=$PATH:$TRIANGLE_PATH` in `.bash_profile` |
| MATLAB cannot find `mutils` | `$MUTILS_PATH` not set | Re-run `source ~/.bash_profile` before launching MATLAB |
| Simulation diverges (NaN) | Viscosity or time-step too large | Lower `dt` or increase `eta_min` in `change_model.m` |
| Out-of-memory error | Mesh too fine for available RAM | Increase `dx_min` or request more memory on the cluster |

For further help, see the [FAQ](faq.md).
