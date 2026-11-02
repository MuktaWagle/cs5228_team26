# Derived data

This directory contains intermediate and final datasets produced from the original `train.csv` and `test.csv` files.

## Files

- `train_location_enriched.csv` and `test_location_enriched.csv` are produced by `Add_location_features.ipynb`. They add HDB location attributes and distances to nearby MRT stations, schools, and shopping malls.
- `train_cleaned_enriched.csv` and `test_cleaned_enriched.csv` are produced by `Data_cleaning.ipynb`. They contain the cleaned feature set used by `Models_main.ipynb`, `Boosting_experiments.ipynb`, and `Error_analysis.ipynb`.

The cleaned files include categorical fields such as `TOWN`, `FLAT_TYPE`, `FLAT_MODEL`, `HDB_PLANNING_AREA`, and `LOCATION_KEY`; numerical and geographic fields such as floor area, lease commencement year, coordinates, building completion year, and nearest-amenity distances; and derived time fields such as `APPROVAL_YEAR`, `APPROVAL_MONTH`, `MONTH_INDEX`, and `BUILDING_AGE`. The training file also includes the target column `MONTHLY_RENT`; the test file does not.

## Reproducing the files

Run `Add_location_features.ipynb` first to create the location-enriched files, then run `Data_cleaning.ipynb` to create the cleaned-enriched files. These notebooks read the original data from the repository root and auxiliary reference files from `auxiliary/`.

The derived CSVs are generated artifacts. If the feature-engineering or cleaning logic changes, regenerate them rather than editing the CSVs manually.
