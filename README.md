# CS5228 Team 26

This repository contains our experiments for predicting HDB monthly rent. The project combines exploratory data analysis, location-based feature engineering, data cleaning, baseline models, boosting models, and error analysis.

## Project workflow

Run the notebooks in this order from the repository root:

1. `EDA_main.ipynb` — inspect the raw train/test data and study feature distributions.
2. `Add_location_features.ipynb` — join HDB block information and calculate distances to MRT stations, schools, and shopping malls.
3. `Data_cleaning.ipynb` — clean the location-enriched data and write the final modeling files.
4. `Models_main.ipynb` — train the mean, Ridge, Random Forest, and CatBoost models using a chronological validation split.
5. `ablation_study.ipynb` — assess the contribution of selected feature groups to CatBoost performance.
6. `Boosting_experiments.ipynb` — compare CatBoost and LightGBM and evaluate a weighted blend.
7. `Error_analysis.ipynb` — examine validation errors by rent band, category, and conflicting records.

The validation split is time-based to mimic forecasting future rents: rows from January 2021 to March 2024 are used for training, and rows from April 2024 to March 2025 are used for validation. The same split is used for the main models, boosting experiments, and error analysis.

## Repository structure

- `train.csv`, `test.csv` — original modeling data.
- `auxiliary/` — HDB block, MRT, school, shopping mall, COE, and stock-price reference data.
- `derived/` — location-enriched and cleaned datasets; see [`derived/README.md`](derived/README.md).
- `plots/` — figures generated during EDA, modeling, and error analysis.
- `predictions/` — model submission files.
- `requirements.txt` — Python package versions captured from the working environment.
- `AI_USAGE.md` — disclosure of AI-assisted development and our responsibility for the final work.
- `*.ipynb` — analysis and modeling notebooks.

## Main outputs

The models use tuned hyperparameters: Ridge `alpha=0.0001`, Random Forest 189 trees with depth 14, CatBoost 1,094 trees with depth 7, and LightGBM 449 trees with 32 leaves. Full settings are saved in [`best_parameters.json`](derived/flaml_tuning/best_parameters.json); the boosting notebook loads LightGBM's settings directly without rerunning the search.

The modeling notebooks write prediction files to `predictions/`, including Ridge, Random Forest, CatBoost, and the CatBoost/LightGBM blend. The blend notebook writes `predictions/catboost_lightgbm_blend_submission.csv`. The ablation and error-analysis notebooks also export summary tables under `derived/error_analysis/` and figures under `plots/`.

## Environment

The notebooks require Python with pandas, NumPy, scikit-learn, CatBoost, LightGBM, matplotlib, and Jupyter. To reproduce the working environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

LightGBM on macOS may also require the OpenMP runtime (`libomp`). Run notebooks from the project root so their relative paths resolve correctly.
