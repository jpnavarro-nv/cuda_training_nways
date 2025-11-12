# 3.2 MPI with CUDA Memcpy

## Implementation Exercise: Part 1

Use the following batch script to replace the direct command `mpirun -np 16 -npersocket 4 ./jacobi_memcpy_mpi -ny 32768`.
Create a file named **`jacobi_memcpy_mpi.sh`** with this content:

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

mpirun -np 8 ./jacobi_memcpy_mpi -ny 32768
```

Submit the job with:

```bash
sbatch jacobi_memcpy_mpi.sh
```

After it completes, inspect the output file **`jacobi_memcpy_mpi_<JOBID>.out`** to review runtime, iteration logs, and any MPI/CUDA messages.

---

## OpenMPI Process Mappings

For mapping experiments, change **only the last `mpirun` line** in the same script as shown below and resubmit each test.

### Per-socket (2 ranks per socket)

```bash
mpirun -np 8 --map-by ppr:2:socket ./jacobi_memcpy_mpi -ny 32768
```

### Per-node (4 ranks per node)

```bash
mpirun -np 8 --map-by ppr:4:node ./jacobi_memcpy_mpi -ny 32768
```

### Per-socket with binding report

```bash
mpirun -np 8 --map-by ppr:2:socket --report-bindings ./jacobi_memcpy_mpi -ny 32768
```

### Per-node with binding report

```bash
mpirun -np 8 --map-by ppr:4:node --report-bindings ./jacobi_memcpy_mpi -ny 32768
```

> Tip: `--report-bindings` prints how ranks are bound to cores/sockets; verify that the placement aligns with your GPU and NUMA topology before comparing timings.
