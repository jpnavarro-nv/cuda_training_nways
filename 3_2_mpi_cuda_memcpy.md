# 3.2 MPI with CUDA Memcpy

## jacobi_memcpy_mpi.sh

```
#!/bin/bash
#SBATCH -p curso
#SBATCH -N 2
#SBATCH --ntasks-per-node=4
#SBATCH --gres=gpu:4
#SBATCH --time=01:00:00
#SBATCH -o jacobi_memcpy_mpi_%j.out

module purge
module load nvhpc-hpcx/23.11

mpirun -np 8 ./jacobi_memcpy_mpi -ny 32768

```
