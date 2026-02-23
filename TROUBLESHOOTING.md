# 🔧 Troubleshooting Guide

Common errors and solutions encountered when setting up environments and running tutorials. If your issue isn't listed here, ask on the [IGWN community forum](https://ask.igwn.org/) or open a [GitHub Issue](https://github.com/asasli/gw-intro-umn/issues).

---

## 🐍 Conda / Python Environment

### ❌ `conda: command not found`
Miniconda is not in your PATH.
```bash
export PATH="$HOME/miniconda3/bin:$PATH"
source ~/.bash_profile   # or ~/.zshrc on Mac
```

### ❌ `conda env create` fails with package conflicts
Try using the libmamba solver:
```bash
conda env create --file igwn-py39.yaml --solver=libmamba
```
Or build a minimal environment manually:
```bash
conda create -n igwn-py39 python=3.9
conda activate igwn-py39
pip install pycbc bilby
```

### ❌ Jupyter doesn't find the conda environment as a kernel
Register it manually:
```bash
conda activate igwn-py39
pip install ipykernel
python -m ipykernel install --user --name igwn-py39 --display-name "IGWN py39"
```
Then restart Jupyter and select the kernel from **Kernel → Change Kernel**.

### ❌ `ModuleNotFoundError` even though package is installed
The notebook is using the wrong kernel. In Jupyter: **Kernel → Change Kernel → select `igwn-py39`**

---

##  PyCBC

### ❌ `ImportError: cannot import name 'get_fd'`
The function name may have changed. Use:
```python
from pycbc.waveform import get_fd_waveform
hp, hc = get_fd_waveform(approximant='IMRPhenomD', ...)
```
Check the [PyCBC documentation](https://pycbc.org/pycbc/latest/html/pycbc.waveform.html) for the current API.

### ❌ GSL errors or LAL-related crashes
Source the IGWN environment before launching Jupyter:
```bash
source /cvmfs/oasis.opensciencegrid.org/ligo/sw/conda/etc/profile.d/conda.sh
conda activate igwn-py39
```

### ❌ PyCBC install fails on Apple Silicon (M1/M2/M3 Mac)
Use Rosetta emulation via conda:
```bash
CONDA_SUBDIR=osx-64 conda create -n igwn-py39 python=3.9
conda activate igwn-py39
conda config --env --set subdir osx-64
pip install pycbc
```

---

##  Bilby

### ❌ Sampler not found
Make sure the sampler backend is installed:
```bash
pip install dynesty     # nested sampling (recommended)
pip install emcee       # MCMC
pip install pymultinest # MultiNest (requires additional C libs)
```

### ❌ Results look wrong or priors not respected
Common causes:
- Priors not correctly defined — check the Bilby prior file syntax
- Data segment too short — edge effects can corrupt the likelihood
- Wrong reference frequency — must match the waveform approximant

---

## CVMFS

### ❌ `cvmfs_config probe` fails
```bash
# Linux
sudo systemctl restart autofs

# Mac — re-mount manually
sudo mount -t cvmfs gwosc.osgstorage.org /cvmfs/gwosc.osgstorage.org
```

### ❌ `/cvmfs/` directory appears empty
```bash
sudo cvmfs_config reload
cvmfs_config probe gwosc.osgstorage.org
```

> **Note:** On Mac, the mount commands in `setup/set_up.md` (steps 17, 19, 21) need to be re-run after every reboot.

---

## 🔐 SSH / Cluster Access

### ❌ `Permission denied (publickey)`
Your key is not loaded:
```bash
ssh-add ~/.ssh/id_ed25519
ssh -T git@github.com   # test
```

### ❌ Kerberos: `kinit` fails or ticket expired
```bash
klist                                    # check status
kinit firstname.lastname@LIGO.ORG        # renew ticket
```

### ❌ `Host key verification failed`
The cluster's key changed. Remove the old entry and reconnect:
```bash
ssh-keygen -R ldas-grid.ligo.caltech.edu
ssh albert.einstein@ldas-grid.ligo.caltech.edu
```

---

## 📓 Jupyter Notebooks

### ❌ Kernel dies immediately
Usually a memory issue:
- Reduce data segment length
- Close other running notebooks
- Check available RAM: `htop` or `free -h`

### ❌ Notebook file is too large to commit to git
Clear outputs before committing:
```bash
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace notebook.ipynb
```

---

## 💬 Still Stuck?

| Resource | Link |
|---|---|
| IGWN community forum | [ask.igwn.org](https://ask.igwn.org/) |
| GitHub Issues | [Open an issue](https://github.com/asasli/gw-intro-umn/issues) |
| LIGO cluster support | `ldas_admin_cit@ligo.caltech.edu` |
| PyCBC documentation | [pycbc.org](https://pycbc.org/pycbc/latest/html/) |
| Bilby documentation | [lscsoft.docs.ligo.org/bilby](https://lscsoft.docs.ligo.org/bilby/) |
