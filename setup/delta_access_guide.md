# NCSA Delta — ACCESS Allocation & Slurm Guide

> A quick-start guide for students in the UMN GW group who need to run jobs on [NCSA Delta](https://docs.ncsa.illinois.edu/systems/delta/en/latest/) via [ACCESS](https://access-ci.org/).

---

## 📋 Table of Contents

- [Prerequisites](#-prerequisites)
- [Step 1 — Get an ACCESS Account](#step-1--get-an-access-account)
- [Step 2 — Join the Allocation](#step-2--join-the-allocation)
- [Step 3 — Find Your NCSA Username](#step-3--find-your-ncsa-username)
- [Step 4 — Set Up NCSA Password & Duo MFA](#step-4--set-up-ncsa-password--duo-mfa)
- [Step 5 — Log In to Delta](#step-5--log-in-to-delta)
- [Step 6 — Find Your Account Name for Slurm](#step-6--find-your-account-name-for-slurm)
- [Step 7 — Submit Jobs with Slurm](#step-7--submit-jobs-with-slurm)
- [Common Slurm Commands](#-common-slurm-commands)
- [Example Batch Scripts](#-example-batch-scripts)
- [Useful Links](#-useful-links)
- [Troubleshooting](#-troubleshooting)

---

## ✅ Prerequisites

Before you begin, make sure you have:

1. A valid institutional email address (`.edu`).
2. Your PI (advisor) has an active ACCESS allocation on Delta — ask them for the **allocation/project ID** (e.g., `PHY240XXX`).
3. Basic familiarity with the terminal and SSH (see [setup/bash_intro.md](bash_intro.md) if needed).

---

## Step 1 — Get an ACCESS Account

1. Go to the [ACCESS user portal](https://access-ci.org/): click **Register** (or **Log In** if you already have one).
2. Register using your university credentials via CILogon.
3. Complete your ACCESS profile (name, email, institution).

> 💡 Your ACCESS account is **separate** from your NCSA account. You need both.

---

## Step 2 — Join the Allocation

Your PI needs to **add you** to the project allocation. Ask your advisor to:

1. Go to [ACCESS Allocations](https://allocations.access-ci.org/).
2. Navigate to their project → **Manage Users** → **Add User**.
3. Add you by your ACCESS username or email.

Once added, you should receive a confirmation email. It can take **up to a few hours** for your NCSA account to be created after being added.

---

## Step 3 — Find Your NCSA Username

Your NCSA username is different from your ACCESS username. To find it:

1. Log in to the [ACCESS portal](https://access-ci.org/).
2. Go to your [ACCESS Profile](https://support.access-ci.org/user/profile).
3. Scroll to the bottom — look for the **"Resource Provider Site Usernames"** table.
4. Find the entry for **Delta** / **NCSA** — that is your NCSA username.

> ⚠️ If you don't see an NCSA username, your account may not have been created yet. Wait a few hours after being added to the allocation, or contact `help@ncsa.illinois.edu`.

---

## Step 4 — Set Up NCSA Password & Duo MFA

Delta requires **NCSA Duo multi-factor authentication (MFA)**, which is separate from your university Duo.

1. **Set/reset your NCSA password**: go to [NCSA Identity](https://identity.ncsa.illinois.edu/) and follow the password reset instructions.
2. **Enroll in NCSA Duo MFA**: follow the instructions on the NCSA Identity page to set up Duo on your phone.

> ⚠️ Your NCSA Duo is **not** the same as your UMN or university Duo. You must enroll separately.

---

## Step 5 — Log In to Delta

SSH into a Delta login node using your **NCSA username**:

```bash
ssh <ncsa_username>@login.delta.ncsa.illinois.edu
```

You will be prompted for:
1. Your **NCSA password**.
2. **NCSA Duo MFA** — either enter a passcode from the Duo app, or type `1` and press Enter to get a push notification.

> 💡 SSH key-pair login is **disabled** on Delta for regular users. You must use password + Duo.

If you have trouble connecting, try:
```bash
ssh -o PreferredAuthentications=keyboard-interactive,password <ncsa_username>@login.delta.ncsa.illinois.edu
```

---

## Step 6 — Find Your Account Name for Slurm

Once logged in to Delta, run:

```bash
accounts
```

This will list your available allocation accounts. The output looks something like:

```
Project           Balance (SUs)
---------         -------------
abcd-delta-cpu       50000.00
abcd-delta-gpu      100000.00
```

The values under **"Project"** are the account names you will use with the `-A` / `--account` flag in Slurm. Note:

- Accounts ending in `-cpu` are for CPU partitions.
- Accounts ending in `-gpu` are for GPU partitions.

> ⚠️ If `accounts` returns nothing, your allocation may not be active yet. Contact your PI or `help@ncsa.illinois.edu`.

---

## Step 7 — Submit Jobs with Slurm

Delta uses the **Slurm** workload manager. There are three main ways to run jobs:

### Option A: Batch Job (`sbatch`)

Write a batch script (see [examples below](#-example-batch-scripts)) and submit:

```bash
sbatch my_job.sh
```

### Option B: Interactive Job (`srun`)

Get an interactive shell on a compute node:

```bash
# CPU interactive
srun -A <account_name> --partition=cpu-interactive \
     --nodes=1 --ntasks=1 --cpus-per-task=4 \
     --mem=16g --time=00:30:00 --pty /bin/bash

# GPU interactive (1 GPU)
srun -A <account_name> --partition=gpuA100x4-interactive \
     --nodes=1 --ntasks=1 --cpus-per-task=4 \
     --mem=32g --gpus-per-node=1 --time=00:30:00 --pty /bin/bash
```

### Option C: Resource Allocation (`salloc`)

Allocate resources and run commands using `srun`:

```bash
salloc -A <account_name> --partition=gpuA100x4 \
       --nodes=1 --gpus-per-node=1 --time=01:00:00

# Then run your commands:
srun python my_script.py

# When done:
exit
```

> 💡 Replace `<account_name>` with the account name from the `accounts` command (Step 6).

---

## 🛠 Common Slurm Commands

| Command | Description |
|---------|-------------|
| `sbatch script.sh` | Submit a batch job |
| `squeue -u $USER` | Check your queued/running jobs |
| `scancel <JOBID>` | Cancel a job |
| `sinfo -s` | Show partition summary |
| `accounts` | Show your account names and balances |
| `scontrol show job <JOBID>` | Detailed info about a job |

---

## 📝 Example Batch Scripts

### CPU Job

```bash
#!/bin/bash
#SBATCH --job-name=my_cpu_job
#SBATCH --account=<account_name>       # from `accounts` command
#SBATCH --partition=cpu
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32g
#SBATCH --time=02:00:00                # hh:mm:ss
#SBATCH --output=logs/%j.out
#SBATCH --error=logs/%j.err

module purge
module load anaconda3_cpu
conda activate myenv

python my_script.py
```

### Single-GPU Job (A100)

```bash
#!/bin/bash
#SBATCH --job-name=my_gpu_job
#SBATCH --account=<account_name>       # must end in -gpu
#SBATCH --partition=gpuA100x4
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=64g
#SBATCH --gpus-per-node=1
#SBATCH --time=04:00:00
#SBATCH --output=logs/%j.out
#SBATCH --error=logs/%j.err
#SBATCH --constraint="scratch"

module purge
module load anaconda3_gpu
conda activate myenv

python train.py --config config.yaml
```

### Multi-GPU Job

```bash
#!/bin/bash
#SBATCH --job-name=multi_gpu
#SBATCH --account=<account_name>
#SBATCH --partition=gpuA100x4
#SBATCH --nodes=1
#SBATCH --ntasks=4
#SBATCH --cpus-per-task=16
#SBATCH --mem=0                        # use all memory on the node
#SBATCH --gpus-per-node=4
#SBATCH --time=08:00:00
#SBATCH --output=logs/%j.out
#SBATCH --error=logs/%j.err
#SBATCH --exclusive

module purge
module load anaconda3_gpu
conda activate myenv

srun python -m torch.distributed.launch --nproc_per_node=4 train.py
```

---

## 🔑 Key Partitions on Delta

| Partition | Type | Max Wall Time | Notes |
|-----------|------|---------------|-------|
| `cpu` | CPU batch | 48 hours | 128 cores/node, 256 GB RAM |
| `cpu-interactive` | CPU interactive | 30 minutes | For debugging, testing |
| `gpuA100x4` | GPU batch (4×A100) | 48 hours | 64 cores, 4 GPUs, 256 GB RAM |
| `gpuA40x4` | GPU batch (4×A40) | 48 hours | 64 cores, 4 GPUs, 256 GB RAM |
| `gpuA100x4-interactive` | GPU interactive | 30 minutes | For quick GPU tests |

> 💡 Match your account type to the partition: `-cpu` accounts → `cpu*` partitions, `-gpu` accounts → `gpu*` partitions.

---

## 📂 File Systems

| Path | Purpose | Quota | Backed Up |
|------|---------|-------|-----------|
| `/u/<username>` (`$HOME`) | Config files, scripts | 50 GB | Yes |
| `/projects/<project>` | Shared project data | Allocation-dependent | No |
| `/scratch/<project>` | Large temporary files | 50 TB | **No — purged!** |
| Node-local SSD | Fast scratch during jobs | ~1.5 TB (GPU nodes) | No |

> ⚠️ `/scratch` is purged periodically. Do **not** store important results there long-term.

---

## 🔗 Useful Links

| Resource | URL |
|----------|-----|
| Delta User Guide | https://docs.ncsa.illinois.edu/systems/delta/en/latest/ |
| ACCESS User Portal | https://access-ci.org/ |
| ACCESS Allocations | https://allocations.access-ci.org/ |
| NCSA Identity (password/Duo) | https://identity.ncsa.illinois.edu/ |
| NCSA Support | https://help.ncsa.illinois.edu/ or `help@ncsa.illinois.edu` |
| Delta Open OnDemand (web GUI) | https://ondemand.delta.ncsa.illinois.edu/ |
| Slurm Quick Start | https://slurm.schedmd.com/quickstart.html |

---

## 🔧 Troubleshooting

**"Permission denied" when logging in**
- Double-check you're using your **NCSA username** (not ACCESS username). Find it in your [ACCESS Profile](https://support.access-ci.org/user/profile) under "Resource Provider Site Usernames."

**`accounts` returns nothing**
- Your allocation may not be active yet. Ask your PI to verify you've been added. Wait a few hours after being added for the account to propagate.

**"Invalid account" when submitting a job**
- Make sure you're using the correct account name from `accounts` (e.g., `abcd-delta-gpu`, not just `abcd`).
- Match CPU accounts to CPU partitions and GPU accounts to GPU partitions.

**"can't start new thread" (RuntimeError)**
- If you're running sklearn or other libraries with `n_jobs=-1`, the thread limit on your node/session may be too low. Set `n_jobs=1` or a small number (e.g., `n_jobs=4`).

**Job pending forever**
- Check with `squeue -u $USER`. Common reasons include: insufficient balance (check with `accounts`), requesting more resources than available, or a busy partition.

**Need help?**
- Email `help@ncsa.illinois.edu` with subject line starting with **"Delta:"** and include your username, account name, and job ID.

---

> 📖 Full Delta documentation: https://docs.ncsa.illinois.edu/systems/delta/en/latest/
