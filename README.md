# CUDA Training Nways — Instructions

For this training you’ll need access to an environment with **multiple GPUs** to complete all hands-on activities. The **first section** can be done with a **single node and multiple GPUs**.
Additionally, you will need **NVIDIA Nsight Systems** for the profiling exercises; please make sure it is **installed locally** so you can follow along. Download it here: [NVIDIA Nsight Systems](https://developer.nvidia.com/nsight-systems).

---

## 1) Clone the repository

```bash
git clone https://github.com/openhackathons-org/nways_multi_gpu.git
```

---

## 2) Toolchain: NVIDIA HPC SDK

We’ll use the **NVIDIA HPC SDK** for most experiments. It already includes CUDA versions compatible with these activities.

### Load modules (examples)

**LNCC**

```bash
module load nvhpc/25.1
```

**GAIA**

```bash
module load nvhpc-hpcx/23.11
```

### Check your CUDA version (must be **≤ 12.8**)

```bash
nvcc --version
```

---

## 3) If you’re on a supercomputer (LNCC or GAIA)

Prefer running builds and executions with **`srun`** so you don’t hold resources idle.

---

## 4) Helper function for `srun`

Define a helper to simplify compile/run commands. Adjust `--gres=gpu:<N>` to the number of GPUs needed. For the **first part**, use **1 GPU**.

**LNCC**

```bash
srun_1g() {
  srun -A <ACCOUNT> -p <PARTITION> -N 1 --time=01:00:00 --gres=gpu:1 --pty "$@"
}
```

**GAIA**

```bash
srun_1g() {
  srun -p curso -N 1 --time=00:04:00 --gres=gpu:1 --pty "$@"
}
```

> Replace `<ACCOUNT>` and `<PARTITION>` with the appropriate values for your project/queue.

---

## 5) Sanity check

```bash
srun_1g nvidia-smi
```

---

## 6) Optional: interactive shell

If there are surplus resources available, start an interactive shell:

```bash
srun_1g bash
```
