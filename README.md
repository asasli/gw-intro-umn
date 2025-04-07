# Introduction to GW Research at UMN

## Table of Contents
- [Overview](#overview)
- [Setting Up Environments and LIGO Account](#setting-up-environments-and-ligo-account)
- [Python](#python)
- [Parameter Estimation with MCMC](#parameter-estimation-with-mcmc)
- [Waveform Generation](#waveform-generation)
- [Suggested Papers](#suggested-papers-and-books)
- [Machine Learning in GW Astronomy](#machine-learning-in-gw-astronomy)
- [Workshops and Schools](#Workshops-and-Schools)
- [GPUs](#GPUs)

## Overview
This repository collects essential steps for conducting research in gravitational-wave (GW) astronomy, based on our activities at the University of Minnesota (UMN).
******************
During your educational-trip, I suggest you to have always open the [ask-IGWN page](https://ask.igwn.org/) where you can ask **ANYTHING** about GW!

A good start could be [this page](https://www.gw-openscience.org/path/), in order to start thinking about the GW theory and distinguish some basic characteristics for frequencies, rate, masses etc. This page you provide you some educational links to better understand noise and data, and if you want more data to explore or "hear" [here is your chance](https://labcit.ligo.caltech.edu/~jkanner/aapt/web/resources.html). Now, you have a main idea about what actually are **Gravitational Waves** and their data-challanges.

Want to know more about **How does LIGO detect gravitational waves?**, then click to this [youtube video](https://www.youtube.com/watch?v=X7RJHxeCulY&ab_channel=CraigCahillane).
*********************
## Setting Up Environments and LIGO Account

Detailed instructions for setting up your local machine and creating conda environments with the necessary packages for GW astronomy can be found [here](https://github.com/asasli/gw-intro-umn/blob/main/set_up.md). Additionally, if you need to set up your LIGO/Virgo/KAGRA (LVK) account, follow the guidance provided [here](https://github.com/asasli/gw-intro-umn/blob/main/lvk_account.md). A full detailed google document has been also created by **Andrew Toivonen** for new UMN students ["New Student Onboarding (LIGO)"](https://docs.google.com/document/d/1yelxiE51AHvz1laxDhnbE5thR6ca5b2Am_drCGGpnFY/edit?tab=t.0)

*You may also want to take a look at [bash](https://github.com/asasli/gw-intro-umn/blob/main/bash_intro.md) introdactory.*

## Python

The codes in this repository are developed using the `Python` programming language. If you're new to Python, there are plenty of online resources to help you get started! For a structured introduction, check out this organized repository: [Python Introduction](https://github.com/asasli/Python_Intro_AUTh).

## Parameter Estimation with MCMC

Parameter estimation is a crucial part of GW astronomy, often using techniques like Markov Chain Monte Carlo (MCMC). [Bayesian Inference and MCMC](https://github.com/asasli/BayesMCMC) is a repository that covers very basic concepts. More content for applications GW astronomy is to be added.

## Waveform Generation

Waveform generation is fundamental for comparing theoretical models with observed GW data. This section will provide resources and examples to help you generate GW waveforms. We basically use two different packages, [Bilby](https://lscsoft.docs.ligo.org/bilby/) and [PyCBC](https://pycbc.org/pycbc/latest/html/index.html#). You can find many different tutorials in the website of the mentioned packages. However, a quick overview could be achieved through these tutorials:

> - [BBH waveform generation and injection into gaussian noise using ```Bilby``` package](https://github.com/asasli/gw-intro-umn/blob/main/https://github.com/asasli/gw-intro-umn/blob/main/BBH-Bilby_plus_injection.ipynb), A. Sasli (2024)
> - [BBH waveform generation and injection into gaussian noise using ```PyCBC``` package](https://github.com/asasli/gw-intro-umn/blob/main/BBH-PyCBC_plus_injection.ipynb), A. Sasli (2024)
> - [BNS waveform generation with ```PyCBC``` package](https://github.com/asasli/gw-intro-umn/blob/main/BNS-PyCBC.ipynb), A. Sasli (2024)
> - [Waveforms Tutorial](https://github.com/PatriciaSchmidt/GWATUT-waveforms), P. Schmidt, G. Pratten (2021)

*Note: I would suggest to take a look at all the above tutorials, because they might have some information that is not included in another tutorial!*

## Suggested Papers and Books

For an in-depth understanding of GW research, reading the foundational and recent papers in the field is highly recommended. A curated list of suggested papers will be added here soon.

### Books

> - [Gravitational-Wave Astronomy](https://global.oup.com/academic/product/gravitational-wave-astronomy-9780198568032?cc=gr&lang=en&), N. Andersson (2021)
> - [Gravitational Waves, Vol. 1](https://oxford.universitypressscholarship.com/view/10.1093/acprof:oso/9780198570745.001.0001/acprof-9780198570745), M. Maggiore (2007)
> - [Gravitational Waves, Vol. 2](https://oxford.universitypressscholarship.com/view/10.1093/oso/9780198570899.001.0001/oso-9780198570899), M. Maggiore (2018)

### Data analysis overview papers and tutorials
> - [A guide to LIGO–Virgo detector noise and extraction of transient gravitational-wave signals](https://iopscience.iop.org/article/10.1088/1361-6382/ab685e) and [codes](https://github.com/gw-odw/Data-Guide-Paper), Abbott et al. (2020)
> - [A Roadmap to Gravitational Wave Data Analysis](https://www.nature.com/articles/s41550-022-01849-y), L. Speri et. al (2022)

> - A very simple tutorial using ```PyCBC``` for BBH PE, can be found [here](https://github.com/asasli/gw-intro-umn/blob/main/data_analysis/BBH_Signal_Injection_and_Recovery_Tutorial.ipynb), A. Sasli (2024).

> - [Parameter estimation on GW150914 using open data](https://colab.research.google.com/github/gw-odw/odw-2019/blob/master/Day_2/Tuto_2.4_Parameter_estimation_for_compact_object_mergers.ipynb)
> - [Bilby Examples and Tutorials](https://git.ligo.org/lscsoft/bilby/-/tree/master/examples)

### Papers related to our group activities
#### GWs & ML
> - [Aframe: A machine-learning pipeline for real-time detection of gravitational waves from compact binary coalescences](https://arxiv.org/html/2403.18661v1)
> - [Amplfi: Rapid Likelihood Free Inference of Compact Binary
Coalescences using Accelerated Hardware](https://arxiv.org/abs/2407.19048)
> - [GWAK: Gravitational-Wave Anomalous Knowledge with Recurrent Autoencoders](https://arxiv.org/abs/2309.11537) & [O3 analysis](https://arxiv.org/pdf/2412.19883)
#### Stochastic GW Background
> - [TBS: The optimal search for an astrophysical gravitational-wave background](https://arxiv.org/abs/1712.00688)
> - A paper from Xiao-Xaio Kou is coming soon!
#### Heavy-tailed likelihoods in GW Astronomy
> - [Heavy-tailed likelihoods for robustness against data outliers: Applications to the analysis of gravitational wave data](https://arxiv.org/abs/2305.04709)
> - [Characterization of non-Gaussian stochastic signals with heavier-tailed likelihoods](https://arxiv.org/abs/2410.14354)
> - A new robust and fast statistical framework for GW astronomy (paper is coming soon!)
#### ML for optical dat
> - [AstroM^3: A self-supervised multimodal model for astronomy](https://arxiv.org/abs/2411.08842)
> - [BTSbot: Automated Identification and Follow-up of Bright Transients with Deep Learning](https://iopscience.iop.org/article/10.3847/1538-4357/ad5666)
> - GitHub Repo for our study (a paper is coming soon):[Apple Cider](https://github.com/ajunell/AppleCider)

## GW tutorials
> - [PyCBC-Tutorials](https://github.com/gwastro/PyCBC-Tutorials/tree/master/tutorial)
> - [LISA Analysis Tools (Tutorials from LATW)](https://github.com/mikekatz04/LATW/tree/main), M. Katz, N. Karnesis, N. Korsakova, A. Sasli, A. Nilsson, R. Tenorio, D. Rai, C. Chapman-Bird (2024).

## Machine Learning \& GW Astronomy

Machine learning is becoming increasingly important in GW research for tasks such as signal classification, noise reduction, and parameter estimation. UMN and MIT group have developed tools and ML algorithms for such purposes. For more details, please visit [ML4GW repository](https://github.com/ML4GW)

> - [Big Data in Astrophysics](https://github.com/mcoughlin/ast8581_2025_Spring), M. W. Coughlin
> - [Deep learning tutorial for Parameter Estimation (Galactic Binary)](https://github.com/NataliaKor/tutorial), N. Korsakova
> - [ML Tutorial for ML Mock Data Challenge](https://github.com/gwastro/ml-mock-data-challenge-1/tree/master/tutorials/Machine%20Learning)
> - [ML4GW tutorial](https://github.com/wbenoit26/ml4gw_tutorial), W. Benoit

## Workshops and Schools

> - [GW Open Data Workshop](https://github.com/gw-odw)


## GPUs
> - [A notebook-based GPU tutorial designed for Google Colab](https://github.com/mikekatz04/GPU_and_GWs_Tutorial), M. Katz
