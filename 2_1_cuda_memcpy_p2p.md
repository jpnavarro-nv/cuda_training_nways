# 2.1 CUDA Training Nways — Multi-GPU Instructions

For this section you’ll need access to **multiple GPUs**. Adjust your `srun` scripts to use **2 or 4 GPUs**, depending on resource availability. The examples below show a **4-GPU** request on **LNCC** and **GAIA**—update the `--gres=gpu:<N>` value to match what you can allocate.

---

## 1) Helper function for multi-GPU `srun`

Adjust `--gres=gpu:<N>` to the number of GPUs needed (2 or 4).

**LNCC (example with 4 GPUs)**

```bash
srun_4g() {
  srun -A <ACCOUNT> -p <PARTITION> -N 1 --time=04:00:00 --gres=gpu:4 --pty "$@"
}
```

**GAIA (example with 4 GPUs)**

```bash
srun_4g() {
  srun -p curso -N 1 --time=04:00:00 --gres=gpu:4 --pty "$@"
}
```

> Replace `<ACCOUNT>` and `<PARTITION>` with the appropriate values for your project/queue, and change `--gres=gpu:<N>` to match the number of GPUs you intend to use.

---

## 2) Sanity check (confirm multiple GPUs)

```bash
srun_4g nvidia-smi
```

You should see multiple GPUs listed in the output.

---

