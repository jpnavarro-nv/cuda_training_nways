# CUDA-aware MPI

## Implementation Exercise: Part 2

Save the following content to `jacobi_cuda_aware_mpi.sh`:

```bash
#!/bin/bash
#SBATCH -p curso
#SBATCH -N 2
#SBATCH --ntasks-per-node=4
#SBATCH --gres=gpu:4
#SBATCH --time=01:00:00
#SBATCH -o jacobi_cuda_aware_mpi_%j.out

module purge
module load nvhpc-hpcx/23.11

mpirun -np 8 --map-by ppr:2:socket ./jacobi_cuda_aware_mpi -ny 32768
```

> Note: `--map-by ppr:2:socket` launches 2 MPI ranks per socket (total of 8 ranks across 2 nodes). Ensure the binary name and CLI flags are spaced exactly as shown.

## Submit the job

```bash
sbatch jacobi_cuda_aware_mpi.sh
```

---

## Increase iterations and compare the results

Edit only the last line of the script to raise the iteration count and resubmit. The higher iteration count increases the compute-to-communication ratio, so **efficiency should improve**.

```bash
mpirun -np 8 --map-by ppr:2:socket ./jacobi_cuda_aware_mpi -ny 32768 -niter 5000
```

After both runs complete, compare the reported timings/throughput in the output files (e.g., `jacobi_memcpy_mpi_<jobid>.out`) to confirm the efficiency gain.

---

## GPUDirect RDMA

Update your previous `sbatch` to allocate a single MPI rank and one GPU per node:

```bash
#SBATCH --ntasks-per-node=1
#SBATCH --gres=gpu:1
```

### Run with GDR enabled (10,000 iterations)

```bash
mpirun -np 2 --map-by ppr:1:node \
  ./jacobi_cuda_aware_mpi -ny 128 -skip_single_gpu -niter 10000
```

### Run with GDR disabled

```bash
mpirun -np 2 --map-by ppr:1:node \
  -x UCX_IB_GPU_DIRECT_RDMA=no \
  ./jacobi_cuda_aware_mpi -ny 128 -skip_single_gpu -niter 10000
```

