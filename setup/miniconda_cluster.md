# 🐍 Installing Miniconda on a Cluster

A step-by-step guide for first-time cluster users. No prior Linux experience required.

---

## ❓ What is Miniconda and Why Do You Need It?

When you log into a cluster, you share the machine with many other users. You cannot install packages system-wide. **Miniconda** solves this by giving you a **personal Python environment** inside your home directory where you can install anything you need — without affecting anyone else and without needing administrator (root) access.

Think of it as a self-contained Python installation that lives in your home folder.

---

## Overview of Steps

```
1. Log in to the cluster
2. Download Miniconda installer
3. Run the installer
4. Restart your shell
5. Verify the installation
6. Create a GW research environment
7. Install packages
8. Register the environment as a Jupyter kernel
```

---

## Step 1 — Log in to the Cluster

From your local machine:

```bash
ssh your_username@cluster_address
```

For LIGO clusters (after setting up Kerberos — see [lvk_account.md](lvk_account.md)):

```bash
ssh albert.einstein@ldas-grid.ligo.caltech.edu
```

Once logged in, you should see a prompt like:
```
[albert.einstein@ldas-pcdev1 ~]$
```

Check which directory you are in (should be your home directory):
```bash
pwd
# Output: /home/albert.einstein
```

---

## Step 2 — Download the Miniconda Installer

We download the **Linux 64-bit** version directly onto the cluster.

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
```

> **What does this do?** `wget` downloads a file from the internet. `-O ~/miniconda.sh` saves it as `miniconda.sh` in your home directory.

Verify it downloaded correctly:
```bash
ls -lh ~/miniconda.sh
# You should see a file around 100–120 MB
```

---

## Step 3 — Run the Installer

```bash
bash ~/miniconda.sh -b -p $HOME/miniconda3
```

> **Flags explained:**
> - `-b` → batch mode (no interactive prompts, accepts license automatically)
> - `-p $HOME/miniconda3` → installs into `/home/your_username/miniconda3`

This will take 1–2 minutes. You will see lines like:
```
PREFIX=/home/albert.einstein/miniconda3
Unpacking payload ...
```

---

## Step 4 — Initialise Conda and Restart Your Shell

Tell conda to set itself up for your shell:

```bash
$HOME/miniconda3/bin/conda init bash
```

Now **reload your shell** to apply the changes:

```bash
source ~/.bashrc
```

You should now see `(base)` at the beginning of your prompt:
```
(base) [albert.einstein@ldas-pcdev1 ~]$
```

This means conda is active. `base` is the default environment — **do not install research packages here**. Always create a dedicated environment (Step 6).

---

## Step 5 — Verify the Installation

```bash
conda --version
# Output: conda 24.x.x  (any recent version is fine)

python --version
# Output: Python 3.x.x

which python
# Output: /home/albert.einstein/miniconda3/bin/python
```

All three commands should work without errors. If `conda: command not found` appears, run:
```bash
source ~/.bashrc
```

---

## Step 6 — Create a GW Research Environment

Never work in the `base` environment. Create a dedicated one:

```bash
conda create -n igwn-py310 python=3.10 -y
```

> This creates an environment called `igwn-py310` with Python 3.10. The `-y` flag automatically confirms the installation.

Activate it:
```bash
conda activate igwn-py310
```

Your prompt changes to:
```
(igwn-py310) [albert.einstein@ldas-pcdev1 ~]$
```

To deactivate when you are done:
```bash
conda deactivate
```

---

## Step 7 — Install GW Research Packages

With `igwn-py310` active:

```bash
# Add the conda-forge channel (has most scientific packages)
conda config --add channels conda-forge
conda config --set channel_priority strict

# Core scientific stack
conda install numpy scipy matplotlib jupyter -y

# GW-specific packages
pip install pycbc
pip install bilby
pip install gwpy gwosc

# Optional but useful
pip install astropy corner umap-learn
```

> **Why `pip` for some packages?** PyCBC and Bilby are best installed via pip as conda versions can lag behind.

Verify everything works:
```bash
python -c "import pycbc; print('PyCBC:', pycbc.__version__)"
python -c "import bilby; print('Bilby:', bilby.__version__)"
python -c "import numpy; print('NumPy:', numpy.__version__)"
```

---

## Step 8 — Register as a Jupyter Kernel

So Jupyter notebooks can find your environment:

```bash
pip install ipykernel
python -m ipykernel install --user --name igwn-py310 --display-name "IGWN Python 3.10"
```

Now when you open JupyterLab or Jupyter Notebook, you will see **"IGWN Python 3.10"** as a kernel option.

Launch Jupyter (if available on the cluster):
```bash
jupyter lab --no-browser --port=8888
```

Then from your **local machine**, set up SSH tunneling to view it in your browser:
```bash
ssh -N -L 8888:localhost:8888 your_username@cluster_address
```

Open your browser and go to: `http://localhost:8888`

---

## 🔁 Daily Workflow

Every time you log in and want to use your environment:

```bash
# Log in
ssh your_username@cluster_address

# Activate your environment
conda activate igwn-py310

# Do your work ...

# Deactivate when done
conda deactivate
```

To make activation automatic on login, add this to your `~/.bashrc`:
```bash
echo "conda activate igwn-py310" >> ~/.bashrc
source ~/.bashrc
```

> **Note:** Only do this if you always want this environment active. If you work with multiple environments, activate manually instead.

---

## 📋 Useful Conda Commands

| Command | What it does |
|---|---|
| `conda env list` | List all your environments |
| `conda activate igwn-py310` | Activate an environment |
| `conda deactivate` | Deactivate current environment |
| `conda list` | List packages in current environment |
| `conda install numpy` | Install a package via conda |
| `pip install pycbc` | Install a package via pip |
| `conda remove -n igwn-py310 --all` | Delete an environment entirely |
| `conda update conda` | Update conda itself |
| `conda clean --all` | Free up disk space from cached packages |

---

## ⚠️ Cluster-Specific Notes

### Disk quota
Your home directory on clusters usually has a **disk quota** (e.g., 10–50 GB). Miniconda + environments can take 2–5 GB. Check your usage with:
```bash
du -sh ~/miniconda3
quota -s
```

If you are running low on space, install to scratch instead:
```bash
bash ~/miniconda.sh -b -p /scratch/your_username/miniconda3
```

### Do not run heavy computations on login nodes
The login node (e.g., `ldas-grid`) is shared. For heavy computations, use a compute node or submit a job via HTCondor. Jupyter sessions are fine on `ldas-pcdev*` nodes.

### Modules system
Some clusters use a **modules system** that provides pre-installed software. Check what's available:
```bash
module avail
module load python/3.10   # if available
```

On LIGO clusters, the full IGWN software stack is available via CVMFS:
```bash
source /cvmfs/oasis.opensciencegrid.org/ligo/sw/conda/etc/profile.d/conda.sh
conda activate igwn-py310   # or another igwn environment
```

See [set_up.md](set_up.md) for full CVMFS setup instructions.

---

## 🔧 Troubleshooting

**`conda: command not found` after installation**
```bash
source ~/.bashrc
# or
export PATH="$HOME/miniconda3/bin:$PATH"
```

**`pip install pycbc` fails with compiler error**
```bash
conda install gsl fftw -y    # install C dependencies first
pip install pycbc
```

**Jupyter kernel not found**
```bash
conda activate igwn-py310
python -m ipykernel install --user --name igwn-py310 --display-name "IGWN Python 3.10"
```

**Environment takes too much disk space**
```bash
conda clean --all -y    # removes cached package tarballs
```

For more issues, see [TROUBLESHOOTING.md](../TROUBLESHOOTING.md) or ask on [ask.igwn.org](https://ask.igwn.org/).

---

*Part of the [gw-intro-umn](https://github.com/asasli/gw-intro-umn) repository · setup/ folder*
