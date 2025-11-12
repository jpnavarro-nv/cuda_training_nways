# 3.1 Introduction to MPI and Multi-Node Execution Overview

## Single Node

The recommended way to run MPI jobs on the GAIA/LNCC cluster is via `sbatch` submission scripts. Create a file named `hello_world.sh` with the following content:

```bash
#!/bin/bash
#SBATCH -p curso
#SBATCH -N 1
#SBATCH --ntasks-per-node=2
#SBATCH --gres=gpu:1
#SBATCH --time=01:00:00
#SBATCH -o hello_world_%j.out

module purge
module load nvhpc-hpcx/23.11

mpirun -np 2 ./hello_world
```

Submit the job with:

```bash
sbatch hello_world.sh
```

This command generates an output file named `hello_world_<JOBID>.out` containing the program’s output.

Key flags highlighted above:

* `-N`: number of nodes requested.
* `--ntasks-per-node`: number of tasks per node (in the current setup, one MPI process per GPU).
* `--gres=gpu`: number of GPUs per node.

## Multiple Nodes

Multi-node execution follows the same structure. Adjust the number of nodes, tasks per node, and GPUs as needed. For example:

```bash
#!/bin/bash
#SBATCH -p curso
#SBATCH -N 2
#SBATCH --ntasks-per-node=2
#SBATCH --gres=gpu:2
#SBATCH --time=01:00:00
#SBATCH -o hello_world_%j.out

module purge
module load nvhpc-hpcx/23.11

mpirun -np 4 ./hello_world
```

> Tip: Ensure that `-np` (total MPI processes) equals `-N × --ntasks-per-node`.
