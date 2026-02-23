#  Data Analysis Tutorials

This folder contains tutorials for GW signal analysis, matched filtering, and parameter estimation.

| Notebook | Description | Packages |
|---|---|---|
| [BBH_Signal_Injection_and_Recovery_Tutorial.ipynb](BBH_Signal_Injection_and_Recovery_Tutorial.ipynb) | Inject a BBH signal into noise and recover parameters using matched filtering and MCMC | `PyCBC` |

---

## Prerequisites

Before running these notebooks, make sure you are comfortable with:

- Python basics (NumPy, Matplotlib)
- What a gravitational waveform looks like → [`../waveforms/`](../waveforms/)
- Basic Bayesian inference concepts → [BayesMCMC repo](https://github.com/asasli/BayesMCMC)
- PyCBC installed → [`../setup/set_up.md`](../setup/set_up.md)

---

## What You'll Learn

**BBH Signal Injection & Recovery:**

1. Generate a BBH waveform with known parameters
2. Inject it into simulated Gaussian noise
3. Apply matched filtering to detect the signal
4. Use MCMC to recover the original parameters
5. Visualize posterior distributions for masses and distance

---

## External Resources

| Resource | Description |
|---|---|
| [PE on GW150914 (Colab)](https://colab.research.google.com/github/gw-odw/odw-2019/blob/master/Day_2/Tuto_2.4_Parameter_estimation_for_compact_object_mergers.ipynb) | Hands-on PE with real open data |
| [Bilby examples](https://git.ligo.org/lscsoft/bilby/-/tree/master/examples) | Official Bilby PE examples |
| [GW Open Data Workshop](https://github.com/gw-odw) | Full tutorial series including PE |
