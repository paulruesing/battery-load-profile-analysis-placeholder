# Battery Load Profile Analysis - Python ML Pipeline

> **Privacy notice:** This repository is a public placeholder with a reduced, high-level
> description of the work for public presentation. The full source code remains
> private as it was developed in collaboration with an external energy industry partner
> and cannot be shared publicly. I am happy to walk through the architecture and
> methodology in a private session upon request.

---

## What this project is

A Python machine learning pipeline for **unsupervised segmentation and interpretation
of customer load profiles** from operational field data of residential solar-powered
battery systems, to enable utilisation and profitability insights at scale.

---

## Key ingredients

### Data analysis & preprocessing
- **Multi-year time-series analysis** - processing of large-scale, minute-resolution
  BMS field data (state of charge, power flows, temperature, voltage, current) spanning
  multiple years and hundreds of systems
- **Outlier detection** - identification and handling of anomalous systems prior to
  feature extraction
- **Seasonal feature extraction** - dimensionality reduction via a seasonal
  decomposition strategy, preserving inter-seasonal variation while enabling
  cross-system comparability

### Deep clustering
- **Autoencoder architecture** - deep fully-connected autoencoder with regularised
  latent space (L1/L2 sparsity constraints) for non-linear dimensionality reduction
  and input optimisation
- **Deep Embedded Clustering (DEC)** - joint optimisation of autoencoder embedding
  and cluster assignments via a self-training procedure (KL divergence loss against a
  sharpened target distribution)
- **Deep Separated Clustering (DSC)** - sequential approach applying K-Means on the
  trained autoencoder's latent representation
- **K-Means benchmark** - classical partitioning algorithm used as a performance
  baseline throughout validation

### Cluster evaluation
- **Internal validation metrics** - systematic quantitative evaluation using Silhouette
  Score and Dunn Index, computed across multiple random feature subsets and averaged
  over repeated runs to mitigate stochastic effects
- **Qualitative assessment** - Isomap-based feature space visualisation, kernel density
  estimates, and cumulative distribution function analysis per cluster

### Reference profile extraction
- **Representative profile derivation** - identification of the real system most
  representative of each cluster (minimising squared distance from the cluster median
  across all features), yielding interpretable, non-artificial reference profiles that
  preserve intra-system temporal variation

### Load profile analysis & simulation
- **Seasonal load profile analysis** - computation of average 24-hour SOC and c-rate
  trajectories per reference profile and season, revealing utilisation patterns,
  cycling behaviour, and inter-seasonal differences across customer segments
- **Potential energy simulation** - simulation of foregone energy throughput during
  full-charge states to quantify unrealised storage capacity and identify
  under-utilised customer segments

### Economic modelling
- **Realised energy cost savings** - financial modelling of actual electricity cost
  savings per reference profile, derived from battery energy outflow and dynamic
  spot market electricity prices, net of foregone infeed compensation
- **Potential savings analysis** - economic projection of additional savings achievable
  under improved utilisation, computed from simulated energy profiles and enabling
  cross-system and cross-segment comparison

---

## Stack

| Layer | Technology |
|---|---|
| Language | Python |
| ML / Deep learning | TensorFlow / Keras |
| Cluster benchmarks | scikit-learn |
| Data processing | Pandas, NumPy |
| Scientific utilities | SciPy |
| Visualisation | Matplotlib |
| Environment | Conda |

---

## Context & motivation

Residential PV-battery systems generate rich multi-year operational logs that are rarely
analysed at scale. This pipeline addresses that gap by providing a systematic,
data-driven framework for segmenting diverse usage behaviours into concise, interpretable
reference profiles - directly enabling OEMs to derive insights on battery utilisation,
customer segmentation, and economic potential without relying on assumed operational
behaviour.

---

## Authors

AI for batteries group at RWTH Aachen.

## License

Source code not included in this repository. All rights reserved.
