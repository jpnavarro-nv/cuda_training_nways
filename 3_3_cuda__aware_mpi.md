# CUDA-aware MPI

## 1) Create the `jacobi_cuda_aware_mpi.sh` script

Save the following content to `jacobi_cuda_aware_mpi.sh`:

```bash
#!/bin/bash
#SBATCH -p curso
#SBATCH -N 2
#SBATCH --ntasks-per-node=4
#SBATCH --gres=gpu:4
#SBATCH --time=01:00:00
#SBATCH -o jacobi_memcpy_mpi_%j.out

module purge
module load nvhpc-hpcx/23.11

mpirun -np 8 --map-by ppr:2:socket ./jacobi_cuda_aware_mpi -ny 32768
```

> Note: `--map-by ppr:2:socket` launches 2 MPI ranks per socket (total of 8 ranks across 2 nodes). Ensure the binary name and CLI flags are spaced exactly as shown.

---

## 2) Submit the job

```bash
sbatch jacobi_cuda_aware_mpi.sh
```

---

## 3) Increase iterations and compare the results

Edit only the last line of the script to raise the iteration count and resubmit. The higher iteration count increases the compute-to-communication ratio, so **efficiency should improve**.

```bash
mpirun -np 8 --map-by ppr:2:socket ./jacobi_cuda_aware_mpi -ny 32768 -niter 5000
```

After both runs complete, compare the reported timings/throughput in the output files (e.g., `jacobi_memcpy_mpi_<jobid>.out`) to confirm the efficiency gain.
