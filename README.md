# ML4SCI HEPSIM GSoC 2026 — Quark/Gluon Jet Analysis

**Candidate:** Vennela Varshini Anasoori

**Email:** vennelavarshini07@gmail.com

**GitHub:** [vennelavarshini18](https://github.com/vennelavarshini18)

---

## Overview
This submission is the evaluation task for the **HEPSIM project under ML4SCI GSoC 2026**.
It analyzes the [Pythia 8 Quark and Gluon Jets dataset](https://zenodo.org/records/3164691)
to explore jet substructure, compute physics observables, apply Lorentz boosts, and build
a binary classifier to distinguish quark jets from gluon jets.

---

## What's Inside

### `HEPSIM_Evaluation.ipynb`
A single end-to-end Jupyter notebook covering all four evaluation tasks:

**Part A — Data Loading and Exploration**
- Loaded the dataset and handled zero-padded constituents correctly
- Counted real constituents separately for quark and gluon jets
- Plotted constituent multiplicity distributions, gluon jets have more particles
- Plotted pT and η distributions of the leading constituent per jet

**Part B — Jet Observables**
- Computed jet mass from summed 4-momenta using the invariant mass formula
- Computed jet width, weighted angular spread of constituents around the jet axis
- Computed pT dispersion, how concentrated the energy is among constituents
- Plotted all three distributions comparing quark vs gluon jets

**Part C — Boost to Jet Rest Frame**
- Implemented a vectorized Lorentz boost function using the standard β = p⃗_J / E_J formula
- Verified the boost by confirming total 3-momentum vanishes to numerical precision (< 1e-8 GeV)
- Visualized constituent momenta in the rest frame (px, py) for quark and gluon jets side by side

**Part D — Quark vs Gluon Classifier**
- Built a Gradient Boosted Decision Tree classifier using 5 rest-frame features:
  multiplicity, jet mass, jet width, pT dispersion, leading constituent energy
- Achieved **AUC ~0.87** on held-out test set
- Reported ROC curve, confusion matrix, and feature importances
- Compared rest-frame vs lab-frame performance, results are similar for scalar observables

---

## Key Findings
- Gluon jets have **higher multiplicity** and **larger width** than quark jets
- Quark jets have **higher pT dispersion** — energy is more concentrated in fewer fragments
- **Multiplicity is the single most discriminating feature**
- The Lorentz boost to the rest frame is verified to numerical precision
- Rest-frame features perform comparably to lab-frame features for scalar observables

---

## Dataset
**Pythia 8 Quark and Gluon Jets** — Komiske, Metodiev, Thaler (2019)
Available at: https://zenodo.org/records/3164691
Download `QG_jets_0.npz` and place it in the same directory as the notebook before running.
*(Dataset not included in this repo due to GitHub's 100MB file size limit.)*

---

## Setup
```bash
pip install numpy matplotlib scikit-learn requests jupyter
jupyter notebook HEPSIM_Evaluation.ipynb
```
