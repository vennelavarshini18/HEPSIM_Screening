# ML4SCI HEPSIM GSoC 2026 — Quark vs Gluon Jet Analysis

**Candidate:** Vennela Varshini Anasoori

**Email:** [vennelavarshini07@gmail.com](mailto:vennelavarshini07@gmail.com)

**GitHub:** [vennelavarshini18](https://github.com/vennelavarshini18)

---

## Overview

This is my **HEPSIM evaluation task submission** for ML4SCI GSoC 2026.
I analyze the [Pythia 8 Quark and Gluon Jets dataset](https://zenodo.org/records/3164691), study jet substructure, compute physics observables, boost jets to their rest frame, and build a binary classifier to separate quark and gluon jets.

---

## What’s in the Notebook

### `HEPSIM_Evaluation.ipynb`

A single notebook covering all steps end-to-end.

**Part A — Data Exploration**

* Loaded dataset and handled zero-padded constituents
* Counted real constituents for quark and gluon jets
* Plotted multiplicity distributions — gluons have ~9/4× more particles (Casimir factor C_A/C_F)
* Plotted leading constituent pT, η, φ distributions

**Part B — Jet Observables**

* Computed jet invariant mass from summed 4-momenta
* Computed jet width (pT-weighted angular spread)
* Computed pT dispersion (energy concentration)
* Compared distributions for quark vs gluon jets with physics commentary

**Part C — Boost to Jet Rest Frame**

* Applied vectorized Lorentz boost: β = p⃗_J / E_J, γ = E_J / m_J
* Verified boost numerically (total 3-momentum < 1e-8 GeV)
* Visualized constituents in (px, py) plane for example quark and gluon jets
* Noted qualitative differences: quarks are compact, gluons are broader

**Part D — Quark vs Gluon Classifier**

* Built Gradient Boosted Trees with 5 features: multiplicity, jet mass, width, pT dispersion, leading energy
* Achieved **AUC ≈ 0.80** on test set
* Plotted ROC curve, confusion matrix, and selected working point via max F1-score
* Ranked feature importance — multiplicity dominates
* Compared rest-frame vs lab-frame — scalar features perform similarly; boost is more useful for constituent-level models

---

## Key Observations

| Observable    | Quark Jets | Gluon Jets |
| ------------- | ---------- | ---------- |
| Multiplicity  | lower      | higher     |
| Jet mass      | lower      | higher     |
| Jet width     | narrower   | wider      |
| pT dispersion | higher     | lower      |

* Multiplicity is the most discriminating feature (C_A/C_F = 9/4)
* Boost verified to numerical precision (<1e-8 GeV residual)
* Rest-frame features ≈ lab-frame for scalar observables; boosts are more useful for particle-level architectures (ParticleNet, LorentzNet)

---

## Dataset

**Pythia 8 Quark and Gluon Jets** — Komiske, Metodiev, Thaler (2019)
[Download here](https://zenodo.org/records/3164691)
Place `QG_jets_0.npz` in the notebook directory before running.
*(Not included in repo due to GitHub file size limit.)*

---

## Quick Setup

```bash
pip install numpy matplotlib scikit-learn jupyter
jupyter notebook HEPSIM_Evaluation.ipynb
```

