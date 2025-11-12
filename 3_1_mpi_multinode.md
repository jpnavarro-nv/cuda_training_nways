# 3.1 Introduction to MPI and Multi-Node execution overview

## Single Node

```
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

## Multi Node

## Single Node

```
#!/bin/bash
#SBATCH -p curso
#SBATCH -N 2
#SBATCH --ntasks-per-node=2
#SBATCH --gres=gpu:1
#SBATCH --time=01:00:00
#SBATCH -o hello_world_%j.out

module purge
module load nvhpc-hpcx/23.11

mpirun -np 4 ./hello_world

```
