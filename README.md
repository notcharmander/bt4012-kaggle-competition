# BT4012 In-class Kaggle Competition

## Final submissions

| File | Model | Public ROC-AUC |
|---|---|---|
| `submissions/default_lgbm_plus_louvain_risk.csv` | Default LightGBM rank-averaged with a Louvain community risk model | 0.95292 |
| `submissions/default_lgbm_plus_isolation_forest.csv` | Default LightGBM with an Isolation Forest feature | 0.95034 |

## How to run

1. Use Python 3.13 and install the pinned dependencies:
   ```
   pip install -r requirements.txt
   ```
2. Put the competition files in this folder, next to the notebook:
   ```
   train.csv
   test.csv
   txs_edgelist.csv
   ```
3. Run the notebook from top to bottom, in Jupyter or from the command line:
   ```
   jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=36000 e1155783.ipynb
   ```

A full run takes about 80 minutes on a laptop.

## Notes

- **Saved results.** Slow steps (Optuna tuning, ablations, community detection) save their results to `artifacts/` and reload them on later runs. The folder is not in the repository; a first run creates it. Delete it to recompute everything.
- **Outputs.** Submission files are written to `submissions/`.
- **Determinism.** All models use fixed seeds. LightGBM runs with 4 threads, so a few predictions can differ in their last decimal places between runs; rankings and ROC-AUC are unaffected.
- **macOS.** LightGBM and XGBoost need the OpenMP library (`brew install libomp`). On Linux or Google Colab, `pip install -r requirements.txt` is enough.

## Notebook structure

1. Data exploration
2. Data preprocessing and feature engineering
3. Model development and validation
4. Model exploration and final strategy (five stages, ending with the final submissions)
