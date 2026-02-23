# Waveform Generation Tutorials

This folder contains notebooks for generating gravitational waveforms from compact binary coalescences (CBCs).

| Notebook | Source Type | Package | Description |
|---|---|---|---|
| [BBH-Bilby_plus_injection.ipynb](BBH-Bilby_plus_injection.ipynb) | BBH | `Bilby` | Waveform generation + injection into Gaussian noise |
| [BBH-PyCBC_plus_injection.ipynb](BBH-PyCBC_plus_injection.ipynb) | BBH | `PyCBC` | Waveform generation + injection into Gaussian noise |
| [BNS-PyCBC.ipynb](BNS-PyCBC.ipynb) | BNS | `PyCBC` | Binary neutron star waveform generation |

> 💡 *Each notebook contains slightly different content and tips — reading all three is recommended.*

---

## Key Concepts

### CBC Source Types

| Type | Components | Typical Mass Range | Key Physics |
|---|---|---|---|
| BBH | Two black holes | 5–100+ M☉ | Orbital dynamics, no matter effects |
| BNS | Two neutron stars | 1–3 M☉ | Tidal deformability, matter EOS |
| NSBH | NS + BH | Mixed | Both tidal and mass-ratio effects |

### Common Waveform Approximants

| Approximant | Domain | Best For |
|---|---|---|
| `IMRPhenomD` | Frequency | Non-spinning BBH, fast computations |
| `IMRPhenomXP` | Frequency | Precessing BBH |
| `SEOBNRv4` | Time | Accurate BBH with aligned spins |
| `TaylorF2` | Frequency | BNS and low-mass systems (inspiral only) |
| `IMRPhenomPv2_NRTidal` | Frequency | BNS with tidal deformability |

---

## Prerequisites

- Python basics (NumPy, Matplotlib)
- PyCBC and/or Bilby installed → see [`../setup/set_up.md`](../setup/set_up.md)
- Basic understanding of what gravitational waves are → [gw-openscience.org/path](https://www.gw-openscience.org/path/)

---

## Next Steps

After completing these notebooks, move on to **parameter estimation** → [`../data_analysis/`](../data_analysis/)
