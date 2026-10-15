# Prediction of Mechanical Properties of H13 Tool Steel (LPBF)

Predicting the mechanical properties of H13 tool steel produced by Laser Powder Bed Fusion (LPBF) additive manufacturing from its process parameters, using multi-output Linear Regression.

## Overview

H13 is a widely used tool steel, and its properties after LPBF depend strongly on the process parameters chosen. This project builds a small, interpretable baseline model that maps those parameters to five target properties at once.

**Inputs (features):** Laser Power (W), Scan Speed (mm/s), Hatch Spacing (mm)

**Outputs (targets):** Hardness (Hv), Yield Strength (MPa), Ultimate Tensile Strength (MPa), Ductility (%), Porosity (%)

## Dataset

- Curated manually from 30+ research papers on LPBF of H13 steel (process parameters + reported mechanical properties).
- Stored in `data/` as Excel files.
- Missing values are common because papers report different subsets of properties (see Preprocessing).

## Methodology

1. **Preprocessing (Pandas, NumPy):** handled missing values (mean imputation for Hatch Spacing, Scan Speed and the target columns), dropped Laser Energy Density because of too many missing entries, and dropped Hatch Angle.
2. **Feature selection:** correlation analysis (heatmap) to choose the final three input parameters.
3. **Model:** multi-output `LinearRegression` from scikit-learn, 80/20 train/test split (`random_state=42`).
4. **Evaluation:** MAE and RMSE per target, plus error-vs-prediction residual plots.

## Results (test set)

| Property | MAE |
|---|---|
| Hardness (Hv) | 49.5 |
| Yield Strength (MPa) | 184.7 |
| UTS (MPa) | 301.9 |
| Ductility (%) | 1.44 |
| Porosity (%) | 0.15 |

## Limitations and next steps

- Small dataset with many imputed values, so results are a baseline, not a production model.
- Linear regression cannot capture non-linear process–property relationships; next steps are Random Forest / Gradient Boosting and cross-validation.
- Heat treatment and temperature are not used as features yet.

## Repository structure

```
.
├── README.md
├── requirements.txt
├── prediction_model.ipynb
└── data/
    └── dataset.xlsx
```

## How to run

```bash
git clone https://github.com/AVIdroid/h13-steel-property-prediction.git
cd h13-steel-property-prediction
pip install -r requirements.txt
jupyter notebook prediction_model.ipynb
```

## Tech stack

Python, Pandas, NumPy, scikit-learn, Matplotlib, Seaborn, Jupyter
