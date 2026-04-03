# Introduction to Research at UMN (GWs & Time-Domain)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![PyCBC](https://img.shields.io/badge/PyCBC-latest-green.svg)](https://pycbc.org/)
[![Bilby](https://img.shields.io/badge/Bilby-latest-orange.svg)](https://lscsoft.docs.ligo.org/bilby/)
[![Maintained](https://img.shields.io/badge/Maintained-yes-brightgreen.svg)](https://github.com/asasli/gw-intro-umn)

> A curated onboarding repository for students joining the gravitational-wave research group at the **University of Minnesota (UMN)**. It covers environment setup, waveform generation, parameter estimation, machine learning tools, and more.

---

## 🗺️ Learning Path

**Not sure where to start?** Follow this roadmap based on your background:

```
🟢 COMPLETE BEGINNER
│
├── 1. Read this README top to bottom
├── 2. Set up your environment       →  setup/set_up.md
├── 3. Learn Bash basics             →  setup/bash_intro.md
├── 4. Python refresher              →  github.com/asasli/Python_Intro_AUTh
└── 5. What are GWs?                 →  gw-openscience.org/path

▼
🟡 SOME BACKGROUND
│
├── 6. Waveform generation           →  waveforms/BBH-Bilby_plus_injection.ipynb
├── 7. Inject signals into noise     →  waveforms/BBH-PyCBC_plus_injection.ipynb
└── 8. Bayesian inference basics     →  github.com/asasli/BayesMCMC

▼
🔴 READY FOR RESEARCH
│
├── 9.  Parameter estimation         →  data_analysis/BBH_Signal_Injection_and_Recovery_Tutorial.ipynb
├── 10. GW Open Data Workshop        →  github.com/gw-odw
├── 11. Bilby tutorials              →  git.ligo.org/lscsoft/bilby/-/tree/master/examples
└── 12. Explore group papers         →  see "Papers Related to Our Group" below
```

> 🎧 Want to *hear* gravitational waves? → [Audio samples](https://labcit.ligo.caltech.edu/~jkanner/aapt/web/resources.html)
> 📺 How does LIGO work? → [YouTube](https://www.youtube.com/watch?v=X7RJHxeCulY)
> 💬 Have a question? → [ask-IGWN](https://ask.igwn.org/)

---

## 📋 Table of Contents

- [Getting Started](#-getting-started)
- [Repository Structure](#-repository-structure)
- [Lectures & Courses](#-lectures--courses)
- [Python Resources](#-python-resources)
- [Waveform Generation](#-waveform-generation)
- [Parameter Estimation with MCMC](#-parameter-estimation-with-mcmc)
- [GW Tutorials](#-gw-tutorials)
- [Machine Learning & GW Astronomy](#-machine-learning--gw-astronomy)
- [GPUs](#-gpus)
- [Suggested Papers & Books](#-suggested-papers--books)
- [Papers Related to Our Group](#-papers-related-to-our-group)
- [Contributing](#-contributing)

---

## 🚀 Getting Started

### Environment & Account Setup

| Resource | Description |
|---|---|
| [setup/set_up.md](setup/set_up.md) | Local machine setup, Miniconda, CVMFS, IGWN conda environment |
| [setup/lvk_account.md](setup/lvk_account.md) | LIGO/Virgo/KAGRA account, LDG cluster access, Kerberos |
| [setup/bash_intro.md](setup/bash_intro.md) | Introduction to Bash scripting |
| [New Student Onboarding (LIGO)](https://docs.google.com/document/d/1yelxiE51AHvz1laxDhnbE5thR6ca5b2Am_drCGGpnFY/edit) | Full guide by **Andrew Toivonen** for new UMN students |

> 💡 If you run into any issues during setup, check the [Troubleshooting Guide](TROUBLESHOOTING.md).

### 🔐 SSH Access to Clusters & Private Repositories

When working on LIGO clusters, you'll need SSH key authentication to access private GitHub repositories.

```bash
# 1. Generate SSH key on the cluster
ssh-keygen -t ed25519 -C "your_email@example.com"

# 2. Start SSH agent and add your key
eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519

# 3. Copy your public key → paste into GitHub Settings → SSH keys
cat ~/.ssh/id_ed25519.pub

# 4. Test the connection
ssh -T git@github.com

# 5. Clone using SSH (not HTTPS!)
git clone git@github.com:organization/repository.git
```

> ⚠️ Set correct permissions: `chmod 700 ~/.ssh && chmod 600 ~/.ssh/id_ed25519`

📄 Full guide: [setup/README_SSH_Cluster_Git_Access.md](setup/README_SSH_Cluster_Git_Access.md)

---

## 📁 Repository Structure

```
gw-intro-umn/
│
├── README.md                        ← You are here
├── CONTRIBUTING.md                  ← How to contribute
├── CHANGELOG.md                     ← History of changes
├── TROUBLESHOOTING.md               ← Common errors & fixes
├── LICENSE
│
├── setup/                           ← Environment & account setup
│   ├── README.md
│   ├── set_up.md
│   ├── lvk_account.md
│   ├── bash_intro.md
│   └── README_SSH_Cluster_Git_Access.md
│
├── waveforms/                       ← Waveform generation notebooks
│   ├── README.md
│   ├── BBH-Bilby_plus_injection.ipynb
│   ├── BBH-PyCBC_plus_injection.ipynb
│   └── BNS-PyCBC.ipynb
│
├── data_analysis/                   ← PE & signal recovery notebooks
│   ├── README.md
│   └── BBH_Signal_Injection_and_Recovery_Tutorial.ipynb
│
└── lectures/                        ← Curated lectures & courses
    └── README.md
```

---

## 🎓 Lectures & Courses

See the full curated list in [lectures/README.md](lectures/README.md).

### Highlights

| Resource | Level |
|---|---|
| [GW Open Data Workshop](https://gw-odw.thinkific.com/) | Beginner–Intermediate |
| [Perimeter Institute – GW lectures](https://pirsa.org/search?searchQuery=gravitational+waves) | Intermediate–Advanced |
| [LISA Analysis Tools Workshop (LATW)](https://github.com/mikekatz04/LATW/tree/main) | Intermediate–Advanced |
| [Les Houches GW lecture notes](https://arxiv.org/abs/gr-qc/0501016) | Intermediate |
| [How LIGO detects GWs (YouTube)](https://www.youtube.com/watch?v=X7RJHxeCulY) | Beginner |

---

## 🐍 Python Resources

The code in this repository is written in **Python**. If you're new to Python:

| Resource | Level |
|---|---|
| [Python Introduction (AUTh)](https://github.com/asasli/Python_Intro_AUTh) | Beginner |
| [Python Lectures Notebooks](https://github.com/Morisset/Python-lectures-Notebooks) | Beginner–Intermediate |
| [Big Data in Astrophysics](https://github.com/mcoughlin/ast8581_2025_Spring) | Intermediate |

**Key libraries used in this repo:**
```python
numpy        # Array operations
matplotlib   # Plotting
pycbc        # GW data analysis
bilby        # Bayesian inference for GW
lal          # LIGO Analysis Library
astropy      # Astronomical calculations
```

---

##  Waveform Generation

We use two main packages: [**Bilby**](https://lscsoft.docs.ligo.org/bilby/) and [**PyCBC**](https://pycbc.org/pycbc/latest/html/index.html).

> 💡 *Each notebook contains slightly different content and tips — reading all three is recommended.*

| Notebook | Description | Package |
|---|---|---|
| [BBH-Bilby_plus_injection.ipynb](waveforms/BBH-Bilby_plus_injection.ipynb) | BBH waveform generation & injection into Gaussian noise | `Bilby` |
| [BBH-PyCBC_plus_injection.ipynb](waveforms/BBH-PyCBC_plus_injection.ipynb) | BBH waveform generation & injection into Gaussian noise | `PyCBC` |
| [BNS-PyCBC.ipynb](waveforms/BNS-PyCBC.ipynb) | Binary neutron star waveform generation | `PyCBC` |
| [Waveforms Tutorial](https://github.com/PatriciaSchmidt/GWATUT-waveforms) | General waveform tutorial | Both |

**Common waveform approximants:**

| Approximant | Domain | Use case |
|---|---|---|
| `IMRPhenomD` | Frequency | Non-spinning BBH, fast |
| `IMRPhenomXP` | Frequency | Precessing BBH |
| `SEOBNRv4` | Time | Accurate BBH, aligned spin |
| `TaylorF2` | Frequency | BNS / low-mass systems |
| `IMRPhenomPv2_NRTidal` | Frequency | BNS with tidal deformability |

---

## Parameter Estimation with MCMC

Parameter estimation is a core part of GW astronomy, using Bayesian inference and MCMC to recover source properties.

| Resource | Description |
|---|---|
| [Bayesian Inference & MCMC](https://github.com/asasli/BayesMCMC) | Foundational concepts (our repo) |
| [BBH Signal Injection & Recovery](data_analysis/BBH_Signal_Injection_and_Recovery_Tutorial.ipynb) | Simple BBH PE with PyCBC — A. Sasli (2024) |
| [PE on GW150914 (open data)](https://colab.research.google.com/github/gw-odw/odw-2019/blob/master/Day_2/Tuto_2.4_Parameter_estimation_for_compact_object_mergers.ipynb) | Google Colab tutorial |
| [Bilby Examples](https://git.ligo.org/lscsoft/bilby/-/tree/master/examples) | Official Bilby example collection |
| [EM-GW PE with Eryn (ACME)](https://github.com/asasli/EM-GW-PE-Eryn/tree/main) | Multi-messenger PE — A. Sasli, N. Karnesis (2025) |

**Key parameters in CBC analysis:**
```
Intrinsic:  m₁, m₂ (masses)  ·  χ₁, χ₂ (spins)  ·  Λ₁, Λ₂ (tides, BNS only)
Extrinsic:  d_L (distance)  ·  ι (inclination)  ·  α, δ (sky location)  ·  ψ (polarization)
```

---

## 📚 GW Tutorials

| Resource | Description |
|---|---|
| [GW Open Data Workshop](https://github.com/gw-odw) | Official annual LIGO/Virgo open data tutorials |
| [PyCBC Tutorials](https://github.com/gwastro/PyCBC-Tutorials/tree/master/tutorial) | Comprehensive PyCBC tutorial series |
| [LISA Analysis Tools (LATW)](https://github.com/mikekatz04/LATW/tree/main) | M. Katz, N. Karnesis, N. Korsakova, A. Sasli et al. (2024) |
| [EM-GW PE with Eryn (ACME)](https://github.com/asasli/EM-GW-PE-Eryn/tree/main) | A. Sasli, N. Karnesis (2025) |

---

## 🤖 Machine Learning & GW Astronomy

ML is increasingly central to GW research — for detection, noise characterization, and parameter estimation. See the [ML4GW repository](https://github.com/ML4GW) for tools developed by UMN & MIT.

| Resource | Description |
|---|---|
| [ML4GW Tutorial](https://github.com/wbenoit26/ml4gw_tutorial) | W. Benoit |
| [Deep Learning for PE (Galactic Binary)](https://github.com/NataliaKor/tutorial) | N. Korsakova |
| [ML Mock Data Challenge Tutorial](https://github.com/gwastro/ml-mock-data-challenge-1/tree/master/tutorials/Machine%20Learning) | gwastro |
| [Big Data in Astrophysics](https://github.com/mcoughlin/ast8581_2025_Spring) | M. W. Coughlin |

---

## ⚡ GPUs

| Resource | Description |
|---|---|
| [GPU & GWs Tutorial](https://github.com/mikekatz04/GPU_and_GWs_Tutorial) | Notebook-based GPU tutorial for Google Colab — M. Katz |

---

## 📖 Suggested Papers & Books

### Textbooks

| Title | Author | Year |
|---|---|---|
| [Gravitational-Wave Astronomy](https://global.oup.com/academic/product/gravitational-wave-astronomy-9780198568032) | N. Andersson | 2021 |
| [Gravitational Waves, Vol. 1](https://oxford.universitypressscholarship.com/view/10.1093/acprof:oso/9780198570745.001.0001/acprof-9780198570745) | M. Maggiore | 2007 |
| [Gravitational Waves, Vol. 2](https://oxford.universitypressscholarship.com/view/10.1093/oso/9780198570899.001.0001/oso-9780198570899) | M. Maggiore | 2018 |
| [A First Course in GR](https://www.amazon.com/First-Course-General-Relativity/dp/0521887054) | B. Schutz | 2009 |

### Key Data Analysis Papers

- [A guide to LIGO–Virgo detector noise and extraction of transient GW signals](https://iopscience.iop.org/article/10.1088/1361-6382/ab685e) + [codes](https://github.com/gw-odw/Data-Guide-Paper) — Abbott et al. (2020)
- [A Roadmap to Gravitational Wave Data Analysis](https://www.nature.com/articles/s41550-022-01849-y) — L. Speri et al. (2022)
- [Parameter estimation with Bilby](https://arxiv.org/abs/1811.02042) — Ashton et al. (2019)
- [Parameter estimation with LALInference](https://arxiv.org/abs/1409.7215) — Veitch et al. (2015)

---

## Papers Related to Our Group

### GWs & Machine Learning

- [Aframe: ML pipeline for real-time GW detection from CBCs](https://arxiv.org/html/2403.18661v1)
- [Amplfi: Rapid Likelihood-Free Inference of CBCs](https://arxiv.org/abs/2407.19048)
- [GWAK: GW Anomalous Knowledge with Recurrent Autoencoders](https://arxiv.org/abs/2309.11537) & [O3 analysis](https://arxiv.org/pdf/2412.19883)

### Stochastic GW Background

- [TBS: Optimal search for an astrophysical GW background](https://arxiv.org/abs/1712.00688)
- [Progress toward detection of the GW background from stellar-mass BBHs](https://arxiv.org/abs/2506.14179)

### Heavy-Tailed Likelihoods in GW Astronomy

- [Heavy-tailed likelihoods for robustness against data outliers](https://arxiv.org/abs/2305.04709)
- [Characterization of non-Gaussian stochastic signals](https://arxiv.org/abs/2410.14354)
- [Beyond Gaussian Assumptions: A new robust statistical framework for gravitational-wave data analysis](https://arxiv.org/abs/2602.22074)

### ML for Optical Data

- [AstroM³: Self-supervised multimodal model for astronomy](https://arxiv.org/abs/2411.08842)
- [BTSbot: Automated identification of bright transients](https://iopscience.iop.org/article/10.3847/1538-4357/ad5666)
- [AppleCiDEr I: Multimodal transient classification](https://arxiv.org/abs/2507.16088) → [GitHub](https://github.com/skyportal/applecider)

---

## Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to add tutorials, fix bugs, or improve documentation.

---

<div align="center">
  <sub>Maintained by the GW group at the University of Minnesota</sub>
</div>
