# Installation

This page describes how to set up the environment required to run Rift2Ridge-Arctic simulations.

## Prerequisites

| Dependency | Minimum version | Notes |
|---|---|---|
| MATLAB | R2018b | Required for the core FEM solver |
| Python | 3.7 | Used for pre/post-processing scripts |
| [mutils](https://github.com/garciapintado/mutils) | 0.4-2 | MATLAB utilities library |
| [SuiteSparse](https://people.engr.tamu.edu/davis/suitesparse.html) | any recent | Sparse matrix operations |
| [Triangle](https://www.cs.cmu.edu/~quake/triangle.html) | 1.6 | 2-D triangle mesh generation |

## 1. Install MATLAB

Install MATLAB R2018b or later. Ensure the `matlab` binary is on your `PATH`.

## 2. Install Python 3

Python 3.7 or later is required. On most Linux systems:

```bash
# Debian/Ubuntu
sudo apt-get install python3 python3-pip

# macOS (via Homebrew)
brew install python
```

## 3. Install mutils

```bash
git clone https://github.com/garciapintado/mutils.git ~/Library/MatlabLib/mutils-0.4-2
```

Follow the build instructions in the `mutils` repository.

## 4. Install SuiteSparse

Download SuiteSparse from [Tim Davis's website](https://people.engr.tamu.edu/davis/suitesparse.html) or install via your package manager:

```bash
# Debian/Ubuntu
sudo apt-get install libsuitesparse-dev
```

Place (or link) the SuiteSparse root in `~/Library/MatlabLib/SuiteSparse`.

## 5. Install Triangle

Download the Triangle source from [CMU](https://www.cs.cmu.edu/~quake/triangle.html) and compile:

```bash
cd ~/Library/MatlabLib/triangle
make
```

Ensure the `triangle` binary is on your `PATH`.

## 6. Set Environment Variables

Add the following to your shell profile (e.g., `~/.bash_profile` or `~/.bashrc`):

```bash
export MATLABROOT="/Applications/MATLAB_R2018b.app"       # path to your MATLAB installation
export PATH=$PATH:$MATLABROOT/bin:$HOME/bin

export WORK=$HOME/scratch                                  # model output directory
export MUTILS_PATH=$HOME/Library/MatlabLib/mutils-0.4-2
export SSPARSE_PATH=$HOME/Library/MatlabLib/SuiteSparse

export TRIANGLE_PATH=$HOME/Library/MatlabLib/triangle
export PATH=$PATH:$TRIANGLE_PATH

export PATH="$PATH:$HOME/Library/Python/3.7/bin"
```

Reload your shell:

```bash
source ~/.bash_profile
```

## 7. Clone This Repository

```bash
git clone https://github.com/vntle/Rift2Ridge-Arctic.git
cd Rift2Ridge-Arctic
```

## Verification

After completing the steps above, verify your setup by checking that each binary is accessible:

```bash
matlab -batch "disp('MATLAB OK')"
python3 --version
triangle -h 2>&1 | head -1
```

For a more thorough test, run one of the minimal example cases included under `SIU3P/data` (see [Usage](usage.md)).

## HPC Cluster Notes

On a cluster managed by **SLURM**, load the relevant modules instead of installing software manually:

```bash
module load matlab/R2022b
module load python/3.9
module load suitesparse
```

An example SLURM submission script is provided in the `scripts/` folder. Adapt the `--partition`, `--ntasks`, and memory flags to your cluster.

See also the [Usage](usage.md) guide for batch-mode invocation details.
