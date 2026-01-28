# Collapsing the Copper-Plate Paradox
### UEVF/ASCDE and an OPF-Consistent Fix for MISO's Two-Tier PRA Signals

[![Status](https://img.shields.io/badge/Status-Protocol_Active-success.svg)]()
[![Reproducibility](https://img.shields.io/badge/Annex_E-Compliant-blue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)]()

**Author:** Justin Candler  
**Contact:** [Nousentllc@gmail.com](mailto:Nousentllc@gmail.com)  
**Paper Date:** January 28, 2026

---

## 📖 Abstract
Regional capacity markets often convey contradictory signals: "adequate in aggregate" (Copper Plate) while simultaneously "short and expensive" locally once transfer limits bite. This repository contains the reference implementation for **UEVF/ASCDE**, a valuation framework that resolves this paradox by grounding accreditation in AC-OPF physics and sequencing interconnection queues via reliability value.


This codebase operationalizes the methods described in *Collapsing the Copper-Plate Paradox*, specifically:
1.  **OPF-Consistent Valuation:** Computing local Marginal Reliability Value (MRV) using seasonal AC baselines and sparse DC linearizations (PTDF/LODF).
2.  **UEVF/ASCDE:** Pricing dependable energy with system-aware reliability adders.
3.  **ARQ Fast-Lane:** A "Reliability-First" interconnection sequencing algorithm.
4.  **Quantum-Inspired Overlay:** (Experimental) Regime weighting for robust planning against weather/policy shifts.

---

## 🚀 Key Features

### 1. The "Copper-Plate" Fix
Standard constructs treat the grid as a copper plate. We implement **Deliverability-Conditioned** valuation:
* **Physics:** Uses `PTDF` and `LODF` matrices derived from seasonal AC-OPF baselines.
* **Logic:** Calculates a deliverability scalar $D^{POI} \in (0,1]$ based on transmission headroom.
* **Outcome:** Resources are accredited only for MW that can physically flow to load during scarcity.

### 2. Decision-Grade Reproducibility (Annex E)
This project adheres to the strict QA standards defined in **Annex E** of the manuscript:
* **Determinism:** Fixed seeds for scenarios, SDDP cuts, and LP tie-breaking.
* **Provenance:** All outputs are stamped with `env_hash`, `seeds.json`, and `solver.yml`.
* **Tolerances:** Automated gates ensure cost reproducibility $\le \pm 0.05\%$ and MRV stability $\le \pm 1.0\%$.

### 3. ARQ Interconnection Sequencing
We include the logic for the **Attribute-Based Reliability Queue (ARQ)**, which ranks projects by a multi-objective score:
$$S = w_1 \cdot \text{Reliability Lift} + w_2 \cdot \text{Survival} + w_3 \cdot \text{Deliverability} - w_4 \cdot \text{Upgrade Cost}$$

## Experimental Features
The Quantum-Inspired Regime Reweighting (Sec 13.2) is included as an experimental overlay.

Status: Prototype / Non-Production.

Activation: Set overlay_gamma > 0 in config/experiment.json.

Note: By default, the system runs in "Classical SDDP" mode (γ=0).

## Citation
If you use this codebase or the UEVF/ASCDE framework, please cite:

Latex Block

@techreport{Candler2026,
  title={Collapsing the Copper-Plate Paradox: UEVF/ASCDE and an OPF-Consistent Fix for MISO's Two-Tier PRA Signals},
  author={Candler, Justin},
  year={2026},
  institution={Nous Energy},
  note={Available at GitHub: [Repository URL]}
}
## License
This project is licensed under the MIT License - see the LICENSE file for details. Audit Tokens: [C00], [LCOE_Guard], [RA_VOLL], [D_POI]
