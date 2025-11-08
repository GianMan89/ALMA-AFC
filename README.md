# ALMA-AFC
Code and datasets for the Adaptive Lifecycle Management Framework for Alarm Flood Classification (ALMA).
Compact, reproducible code and results for **adaptive Alarm Flood Classification (AFC)** using **Asset Administration Shell (AAS)** + **MLOps**.
This repository accompanies the manuscript “Asset Administration Shell-Based MLOps Framework for Adaptive Alarm Flood Classification” (submitted to IFAC World Congress 2026).

---

## 📁 Repository Layout
```
ALMA-AFC/
├─ classifiers/           # Reference implementations of AFC baselines
│  ├─ AFC.py              # Common interfaces / utilities
│  ├─ WDI_1NN.py
│  ├─ ACM_SVM.py
│  ├─ CASIM.py
│  ├─ CASIM_arsenal.py
│  ├─ CASIM_multirocket.py
│  ├─ EAC_1NN.py
│  └─ MBW_LR.py
├─ data/
│  ├─ fcc/                # Place preprocessed FCC files here
│  └─ tep/                # Place preprocessed TEP files here
├─ results/               # Aggregated CV results per model & dataset (CSV)
│  ├─ fcc_results_acm_svm.csv
│  ├─ fcc_results_casim.csv
│  ├─ fcc_results_eac_1nn.csv
│  ├─ fcc_results_mbw_lr.csv
│  ├─ fcc_results_wdi_1nn.csv
│  ├─ tep_results_acm_svm.csv
│  ├─ tep_results_casim.csv
│  ├─ tep_results_eac_1nn.csv
│  ├─ tep_results_mbw_lr.csv
│  └─ tep_results_wdi_1nn.csv
├─ evaluation.ipynb       # End-to-end training/evaluation & perturbations
├─ visualization.ipynb    # Plots (accuracy–distance curves, summaries)
├─ requirements.txt       # Python dependencies
├─ LICENSE
└─ README.md              # This file
```

---

## 🚀 Quick Start
1) Create and activate a virtual environment:
   - Linux/macOS: `python -m venv .venv && source .venv/bin/activate`
   - Windows:     `py -m venv .venv && .\.venv\Scripts\activate`
2) Install deps: `pip install -U pip && pip install -r requirements.txt`
3) Prepare data:
   - Put TEP preprocessed files under `data/tep/`
   - Put FCC preprocessed files under `data/fcc/`
   - (Raw datasets are not redistributed; see paper/links for sources.)
4) Run experiments: open `evaluation.ipgynb` and execute all cells.
5) Inspect/plot results: open `visualization.ipynb` (generates figures and summaries).

Python ≥ 3.9 recommended.

---

## 📦 Results (CSV schema)
Each `results/*_results_*.csv` contains rows with:
- `dataset_version` : `"__benchmark__"` or a perturbed version id
- `evaluation`      : `"benchmark_model"` or `"alt_model"`
- `split`           : `"val"` or `"test"`
- `accuracy`        : mean CV accuracy (optionally `accuracy_std`)
- `dataset_distance_to_benchmark` : float distance to baseline configuration

Helper utilities in `visualization.ipynb` provide:
- Aggregated accuracy–vs–distance curves with shared quantile binning + 95% CI
- Confidence-ellipse summaries (optional)
- Selection-strategy evaluation (benchmark-only vs alt-only vs AAS/MLOps-guided)

---

## 🧠 Implemented AFC Baselines
- **Set-based:** `WDI_1NN`
- **Sequence-based:** `EAC_1NN`, `MBW_LR`
- **Series/shape-based:** `ACM_SVM`, `CASIM` (+ `CASIM_arsenal`, `CASIM_multirocket`)
All models share a minimal interface in `classifiers/AFC.py`.

---

## 🔧 Extending
- Add new models under `classifiers/` (follow the `AFCModel` pattern).
- Add new datasets under `data/<name>/` and update the evaluation notebook.
- Reuse the provided binning/CI and correlation utilities in `visualization.ipynb`.

---

## 📜 License
See `LICENSE`.

---

## 📣 Citation / Status
If you use this repository, please cite:
  Manca, G.; Rezaee Ahvanouee, H.; Faubel-Teich, L.; Kunze, F. C.; and Fay, A.
  “Asset Administration Shell-Based MLOps Framework for Adaptive Alarm Flood Classification.”
  Submitted to **IFRA World Congress 2026** — *manuscript under review at the time of release*.