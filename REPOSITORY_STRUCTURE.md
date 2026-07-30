# Repository Structure and Reproducibility Guide

## 1. Purpose of this document

This repository was reorganized after the analyses were completed.

The original project directory was a working research environment. Its notebooks were written against a specific local folder structure, including several duplicate copies of final datasets placed at the repository root or inside `Background_Data`. Those duplicates were retained in the original layout because the code refers to those exact locations.

The reorganized public repository is arranged for clarity, provenance, and efficient navigation. Raw data, intermediate outputs, manual-review materials, processed datasets, figures, notebooks, and model results are separated into dedicated directories.

The reorganization changed file locations and notebook names. It did not change the underlying data values, analyses, figures, or reported results.

Two layouts therefore exist:

- **Original working layout:** preserves the paths expected by the notebooks as originally written.
- **Reorganized public layout:** consolidates duplicate files and presents the project in a clearer research-repository structure.

## 2. Notebook workflow

The analysis was developed in the following order:

1. `Cathedral_Final_Pipeline.ipynb`
2. `Castle_Data_Self.ipynb`
3. `Pyramids_Pipeline.ipynb`
4. `Combining_And_Manually_Correcting_Dat.ipynb`
5. `Analysis_and_Figures.ipynb`

In the reorganized repository, these notebooks are stored as:

```text
notebooks/
├── 01_cathedral_pipeline.ipynb
├── 02_castle_pipeline.ipynb
├── 03_pyramid_pipeline.ipynb
├── 04_harmonization_and_manual_review.ipynb
└── 05_analysis_and_figures.ipynb
```

The numerical prefixes describe the intended execution order.

## 3. Reorganized public repository

```text
.
├── data/
│   ├── raw/
│   │   ├── cathedrals/
│   │   │   └── cathedral_master.csv
│   │   ├── castles/
│   │   │   └── european_castles_raw.csv
│   │   └── pyramids/
│   │       └── pyramids.csv
│   ├── intermediate/
│   │   ├── caches/
│   │   │   ├── castle_osm_area_cache.json
│   │   │   ├── cathedral_elevation_cache.csv
│   │   │   ├── cathedral_osm_area_cache.json
│   │   │   └── pyramid_elevation_cache.csv
│   │   ├── cathedrals/
│   │   │   ├── cathedral_final_researched_clean.csv
│   │   │   └── cathedral_master_with_wikidata_styles_with_periods.csv
│   │   ├── castles/
│   │   │   ├── european_castles_clean.csv
│   │   │   ├── european_castles_clean_castle_type_with_duration.csv
│   │   │   └── european_castles_clean_castle_type_with_duration_manual_corrected.csv
│   │   └── pyramids/
│   │       ├── pyramids_kaggle_clean.csv
│   │       └── pyramids_Periods.csv
│   ├── manual_review/
│   │   ├── notes/
│   │   │   ├── castle_manual_correction_notes.md
│   │   │   └── cathedral_manual_correction_notes_combined.md
│   │   └── audits/
│   │       ├── applied_cathedral_castle_manual_correction_audit.csv
│   │       ├── cathedral_targeted_research_audit.csv
│   │       ├── dropped_cathedral_castle_manual_correction_audit.csv
│   │       ├── european_castles_duration_one_by_one_check.csv
│   │       ├── kept_rows_without_numeric_correction.csv
│   │       ├── parsed_cathedral_castle_manual_corrections.csv
│   │       └── unmatched_cathedral_castle_manual_corrections.csv
│   └── processed/
│       ├── final_class_specific_datasets/
│       │   ├── cathedral_final_researched_clean_osm_area.csv
│       │   ├── european_castles_osm_area_elevation_enriched.csv
│       │   └── pyramids_kaggle_clean_manual_duration_corrected.csv
│       ├── monuments_harmonized_all.csv
│       ├── monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
│       └── monuments_harmonized_complete_case_positive_duration_pre1750.csv
├── external/
│   └── cathedral_source_reproduction_files/
│       ├── dat/
│       ├── excels/
│       ├── figs/
│       ├── script/
│       ├── tab/
│       ├── README.md
│       └── reproduce.sh
├── figures/
│   ├── construction_duration.png
│   ├── elevation.png
│   ├── feature_space.png
│   └── log_area.png
├── notebooks/
│   ├── 01_cathedral_pipeline.ipynb
│   ├── 02_castle_pipeline.ipynb
│   ├── 03_pyramid_pipeline.ipynb
│   ├── 04_harmonization_and_manual_review.ipynb
│   └── 05_analysis_and_figures.ipynb
├── results/
│   ├── nonlinear_separability_confusion_matrices.csv
│   ├── nonlinear_separability_nested_cv_summary.csv
│   ├── nonlinear_separability_outer_fold_scores.csv
│   ├── nonlinear_separability_selected_parameters.csv
│   ├── separability_oneoff_results_summary.csv
│   ├── separability_repeated_undersampling_30_runs_raw.csv
│   └── separability_repeated_undersampling_30_runs_summary.csv
└── REPOSITORY_STRUCTURE.md
```

Any empty directories with names such as `intermediate 2`, `manual_review 2`, `processed 2`, or `raw 2` are not part of the intended repository structure.

## 4. Original working directory

The original working directory placed notebooks, final class-specific datasets, figures, and result files at or near the repository root:

```text
.
├── Analysis_and_Figures.ipynb
├── Castle_Data_Self.ipynb
├── Cathedral_Final_Pipeline.ipynb
├── Pyramids_Pipeline.ipynb
├── Background_Data/
│   ├── cathedral_master.csv
│   ├── cathedral_master_with_wikidata_styles_with_periods.csv
│   ├── cathedral_final_researched_clean.csv
│   ├── cathedral_final_researched_clean_osm_area.csv
│   ├── cathedral_elevation_cache.csv
│   ├── cathedral_osm_area_cache.json
│   ├── cathedral_targeted_research_audit.csv
│   ├── european_castles_raw.csv
│   ├── european_castles_clean.csv
│   ├── european_castles_clean_castle_type_with_duration.csv
│   ├── european_castles_clean_castle_type_with_duration_manual_corrected.csv
│   ├── european_castles_duration_one_by_one_check.csv
│   ├── european_castles_osm_area_elevation_enriched.csv
│   ├── castle_osm_area_cache.json
│   ├── pyramids.csv
│   ├── pyramids_Periods.csv
│   ├── pyramids_kaggle_clean.csv
│   ├── pyramids_kaggle_clean_manual_duration_corrected.csv
│   ├── pyramid_elevation_cache.csv
│   └── cathedrals/
│       ├── dat/
│       ├── excels/
│       ├── figs/
│       ├── script/
│       ├── tab/
│       ├── README.md
│       └── reproduce.sh
├── Combining_And_Manually_Correcting_Data_Files/
│   ├── Combining_And_Manually_Correcting_Dat.ipynb
│   ├── cathedral_manual_correction_notes_combined.md
│   ├── castle_manual_correction_notes.md
│   ├── monuments_harmonized_all.csv
│   ├── monuments_harmonized_complete_case_positive_duration_pre1750.csv
│   ├── monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
│   ├── parsed_cathedral_castle_manual_corrections.csv
│   ├── applied_cathedral_castle_manual_correction_audit.csv
│   ├── dropped_cathedral_castle_manual_correction_audit.csv
│   ├── unmatched_cathedral_castle_manual_corrections.csv
│   └── kept_rows_without_numeric_correction.csv
├── cathedral_final_researched_clean_osm_area.csv
├── european_castles_osm_area_elevation_enriched.csv
├── pyramids_kaggle_clean_manual_duration_corrected.csv
├── monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
├── construction_duration_alternative_five_panel_broken_axis_log_scale.png
├── elevation_five_panel_broken_axis_log_scale.png
├── log_area_five_panel_broken_axis_layout.png
├── monument_feature_space_clouds_wide.png
├── separability_oneoff_results_summary.csv
├── separability_repeated_undersampling_30_runs_raw.csv
├── separability_repeated_undersampling_30_runs_summary.csv
├── nonlinear_separability_nested_cv_summary.csv
├── nonlinear_separability_outer_fold_scores.csv
├── nonlinear_separability_selected_parameters.csv
└── nonlinear_separability_confusion_matrices.csv
```

The duplicate root-level datasets are intentionally preserved in the original-layout worktree because later notebooks refer to them from those locations.

## 5. Notebook-specific path requirements

### 5.1 Cathedral pipeline

**Original notebook**

```text
Cathedral_Final_Pipeline.ipynb
```

**Current notebook**

```text
notebooks/01_cathedral_pipeline.ipynb
```

The notebook hard-codes:

```python
PROJECT_DIR = Path(
    "/Users/jeeveshattri/Desktop/Monuments_Of_Power/Background_Data"
)
```

It then defines:

```python
REPO_DIR = PROJECT_DIR / "cathedrals"
DAT = REPO_DIR / "dat"
EXCELS = REPO_DIR / "excels"
```

#### Required source files

The first pipeline cell expects:

```text
Background_Data/cathedrals/dat/statobs.csv
Background_Data/cathedrals/dat/heights.csv
Background_Data/cathedrals/dat/dynobs.csv
Background_Data/cathedrals/dat/disasters.csv
Background_Data/cathedrals/dat/italyheights.csv
Background_Data/cathedrals/excels/saints and exogenous disasters.xlsx
```

In the reorganized repository, these files are located at:

```text
external/cathedral_source_reproduction_files/dat/statobs.csv
external/cathedral_source_reproduction_files/dat/heights.csv
external/cathedral_source_reproduction_files/dat/dynobs.csv
external/cathedral_source_reproduction_files/dat/disasters.csv
external/cathedral_source_reproduction_files/dat/italyheights.csv
external/cathedral_source_reproduction_files/excels/saints and exogenous disasters.xlsx
```

#### Outputs from the first cell

The notebook writes:

```text
Background_Data/cathedral_master.csv
Background_Data/cathedral_master_with_wikidata_styles_with_periods.csv
```

Current locations:

```text
data/raw/cathedrals/cathedral_master.csv
data/intermediate/cathedrals/cathedral_master_with_wikidata_styles_with_periods.csv
```

#### Inputs and outputs from the targeted-research cell

The notebook looks for either:

```text
Background_Data/cathedral_master_with_wikidata_styles_with_periods.csv
```

It reads and updates:

```text
Background_Data/cathedral_elevation_cache.csv
```

It writes:

```text
Background_Data/cathedral_final_researched_clean.csv
Background_Data/cathedral_targeted_research_audit.csv
```

Current locations:

```text
data/intermediate/caches/cathedral_elevation_cache.csv
data/intermediate/cathedrals/cathedral_final_researched_clean.csv
data/manual_review/audits/cathedral_targeted_research_audit.csv
```

#### Inputs and outputs from the OSM-area cell

The notebook reads:

```text
Background_Data/cathedral_final_researched_clean.csv
Background_Data/cathedral_osm_area_cache.json
```

It writes:

```text
Background_Data/cathedral_final_researched_clean_osm_area.csv
Background_Data/cathedral_osm_area_cache.json
```

Current locations:

```text
data/intermediate/cathedrals/cathedral_final_researched_clean.csv
data/intermediate/caches/cathedral_osm_area_cache.json
data/processed/final_class_specific_datasets/cathedral_final_researched_clean_osm_area.csv
```

### 5.2 Castle pipeline

**Original notebook**

```text
Castle_Data_Self.ipynb
```

**Current notebook**

```text
notebooks/02_castle_pipeline.ipynb
```

The notebook uses:

```python
PROJECT_DIR = Path(
    "/Users/jeeveshattri/Desktop/Monuments_Of_Power/Background_Data"
)
```

#### Initial Wikidata retrieval

The first cell writes:

```text
Background_Data/european_castles_raw.csv
Background_Data/european_castles_clean.csv
```

Current locations:

```text
data/raw/castles/european_castles_raw.csv
data/intermediate/castles/european_castles_clean.csv
```

#### Castle-type and duration filtering

The next cell reads:

```text
Background_Data/european_castles_clean.csv
```

It writes:

```text
Background_Data/european_castles_clean_castle_type_with_duration.csv
```

Current locations:

```text
data/intermediate/castles/european_castles_clean.csv
data/intermediate/castles/european_castles_clean_castle_type_with_duration.csv
```

#### Manual duration correction

The notebook reads:

```text
Background_Data/european_castles_clean_castle_type_with_duration.csv
Background_Data/european_castles_duration_one_by_one_check.csv
```

It writes:

```text
Background_Data/european_castles_clean_castle_type_with_duration_manual_corrected.csv
```

Current locations:

```text
data/intermediate/castles/european_castles_clean_castle_type_with_duration.csv
data/manual_review/audits/european_castles_duration_one_by_one_check.csv
data/intermediate/castles/european_castles_clean_castle_type_with_duration_manual_corrected.csv
```

#### OSM area and elevation enrichment

The notebook reads:

```text
Background_Data/european_castles_clean_castle_type_with_duration_manual_corrected.csv
```

It can alternatively read:

```text
Background_Data/european_castles_clean_castle_type_with_duration.csv
```

It uses and updates:

```text
Background_Data/castle_osm_area_cache.json
```

It writes:

```text
Background_Data/european_castles_osm_area_elevation_enriched.csv
```

Current locations:

```text
data/intermediate/castles/european_castles_clean_castle_type_with_duration_manual_corrected.csv
data/intermediate/caches/castle_osm_area_cache.json
data/processed/final_class_specific_datasets/european_castles_osm_area_elevation_enriched.csv
```

### 5.3 Pyramid pipeline

**Original notebook**

```text
Pyramids_Pipeline.ipynb
```

**Current notebook**

```text
notebooks/03_pyramid_pipeline.ipynb
```

The notebook uses:

```python
PROJECT_DIR = Path(
    "/Users/jeeveshattri/Desktop/Monuments_Of_Power/Background_Data"
)
```

#### Initial enrichment cell

The notebook reads:

```text
Background_Data/pyramids.csv
```

It uses and updates:

```text
Background_Data/pyramid_elevation_cache.csv
```

It writes:

```text
Background_Data/pyramids_Periods.csv
Background_Data/pyramids_kaggle_clean.csv
```

Current locations:

```text
data/raw/pyramids/pyramids.csv
data/intermediate/caches/pyramid_elevation_cache.csv
data/intermediate/pyramids/pyramids_Periods.csv
data/intermediate/pyramids/pyramids_kaggle_clean.csv
```

#### Manual duration correction cell

The notebook reads:

```text
Background_Data/pyramids_kaggle_clean.csv
```

It writes:

```text
Background_Data/pyramids_kaggle_clean_manual_duration_corrected.csv
```

Current locations:

```text
data/intermediate/pyramids/pyramids_kaggle_clean.csv
data/processed/final_class_specific_datasets/pyramids_kaggle_clean_manual_duration_corrected.csv
```

### 5.4 Harmonization and manual-review notebook

**Original notebook**

```text
Combining_And_Manually_Correcting_Data_Files/
└── Combining_And_Manually_Correcting_Dat.ipynb
```

**Current notebook**

```text
notebooks/04_harmonization_and_manual_review.ipynb
```

This notebook was originally run from:

```text
Combining_And_Manually_Correcting_Data_Files/
```

#### Class-specific inputs

The first cell uses parent-directory references:

```python
cathedral_path = "../cathedral_final_researched_clean_osm_area.csv"
castle_path = "../european_castles_osm_area_elevation_enriched.csv"
pyramid_path = "../pyramids_kaggle_clean_manual_duration_corrected.csv"
```

Therefore, in the original layout, these three files had to exist at the repository root:

```text
cathedral_final_researched_clean_osm_area.csv
european_castles_osm_area_elevation_enriched.csv
pyramids_kaggle_clean_manual_duration_corrected.csv
```

These root-level copies are intentional and path-compatible with the original code.

Their authoritative locations in the reorganized repository are:

```text
data/processed/final_class_specific_datasets/cathedral_final_researched_clean_osm_area.csv
data/processed/final_class_specific_datasets/european_castles_osm_area_elevation_enriched.csv
data/processed/final_class_specific_datasets/pyramids_kaggle_clean_manual_duration_corrected.csv
```

#### Initial harmonization outputs

The first cell writes into its current working directory:

```text
monuments_harmonized_all.csv
monuments_harmonized_complete_case_positive_duration_pre1750.csv
```

In the original layout, these were written to:

```text
Combining_And_Manually_Correcting_Data_Files/
```

Current locations:

```text
data/processed/monuments_harmonized_all.csv
data/processed/monuments_harmonized_complete_case_positive_duration_pre1750.csv
```

#### Manual-review inputs

The second cell reads relative filenames from its current working directory:

```text
monuments_harmonized_complete_case_positive_duration_pre1750.csv
cathedral_manual_correction_notes_combined.md
castle_manual_correction_notes.md
```

Current locations:

```text
data/processed/monuments_harmonized_complete_case_positive_duration_pre1750.csv
data/manual_review/notes/cathedral_manual_correction_notes_combined.md
data/manual_review/notes/castle_manual_correction_notes.md
```

#### Manual-review outputs

The second cell writes:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
parsed_cathedral_castle_manual_corrections.csv
applied_cathedral_castle_manual_correction_audit.csv
dropped_cathedral_castle_manual_correction_audit.csv
unmatched_cathedral_castle_manual_corrections.csv
kept_rows_without_numeric_correction.csv
```

Current locations:

```text
data/processed/monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
data/manual_review/audits/parsed_cathedral_castle_manual_corrections.csv
data/manual_review/audits/applied_cathedral_castle_manual_correction_audit.csv
data/manual_review/audits/dropped_cathedral_castle_manual_correction_audit.csv
data/manual_review/audits/unmatched_cathedral_castle_manual_corrections.csv
data/manual_review/audits/kept_rows_without_numeric_correction.csv
```

#### Pevensey exclusion cell

The final cell reads and overwrites:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

It removes Pevensey Castle and writes the revised dataset back to the same path.

### 5.5 Analysis and figures notebook

**Original notebook**

```text
Analysis_and_Figures.ipynb
```

**Current notebook**

```text
notebooks/05_analysis_and_figures.ipynb
```

This notebook was originally run from the repository root.

It repeatedly reads:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Current authoritative location:

```text
data/processed/monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

#### Construction-duration figure

Input:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Output:

```text
construction_duration_alternative_five_panel_broken_axis_log_scale.png
```

Current output location:

```text
figures/construction_duration.png
```

#### Log-area figure

Input:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Output:

```text
log_area_five_panel_broken_axis_layout.png
```

Current output location:

```text
figures/log_area.png
```

#### Elevation figure

Input:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Output:

```text
elevation_five_panel_broken_axis_log_scale.png
```

Current output location:

```text
figures/elevation.png
```

#### Linear separability and repeated undersampling

Input:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Outputs:

```text
separability_oneoff_results_summary.csv
separability_repeated_undersampling_30_runs_raw.csv
separability_repeated_undersampling_30_runs_summary.csv
```

Current locations:

```text
results/separability_oneoff_results_summary.csv
results/separability_repeated_undersampling_30_runs_raw.csv
results/separability_repeated_undersampling_30_runs_summary.csv
```

#### Shared feature-space figure

Input:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Output:

```text
monument_feature_space_clouds_wide.png
```

Current output location:

```text
figures/feature_space.png
```

#### Nonlinear separability analysis

Input:

```text
monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

Outputs:

```text
nonlinear_separability_nested_cv_summary.csv
nonlinear_separability_outer_fold_scores.csv
nonlinear_separability_selected_parameters.csv
nonlinear_separability_confusion_matrices.csv
```

Current locations:

```text
results/nonlinear_separability_nested_cv_summary.csv
results/nonlinear_separability_outer_fold_scores.csv
results/nonlinear_separability_selected_parameters.csv
results/nonlinear_separability_confusion_matrices.csv
```

## 6. Original-to-current mapping summary

| Original path | Current path |
|---|---|
| `Cathedral_Final_Pipeline.ipynb` | `notebooks/01_cathedral_pipeline.ipynb` |
| `Castle_Data_Self.ipynb` | `notebooks/02_castle_pipeline.ipynb` |
| `Pyramids_Pipeline.ipynb` | `notebooks/03_pyramid_pipeline.ipynb` |
| `Combining_And_Manually_Correcting_Data_Files/Combining_And_Manually_Correcting_Dat.ipynb` | `notebooks/04_harmonization_and_manual_review.ipynb` |
| `Analysis_and_Figures.ipynb` | `notebooks/05_analysis_and_figures.ipynb` |
| `Background_Data/cathedrals/` | `external/cathedral_source_reproduction_files/` |
| `Background_Data/cathedral_master.csv` | `data/raw/cathedrals/cathedral_master.csv` |
| `Background_Data/european_castles_raw.csv` | `data/raw/castles/european_castles_raw.csv` |
| `Background_Data/pyramids.csv` | `data/raw/pyramids/pyramids.csv` |
| `Background_Data/cathedral_final_researched_clean_osm_area.csv` and root-level duplicate | `data/processed/final_class_specific_datasets/cathedral_final_researched_clean_osm_area.csv` |
| `Background_Data/european_castles_osm_area_elevation_enriched.csv` and root-level duplicate | `data/processed/final_class_specific_datasets/european_castles_osm_area_elevation_enriched.csv` |
| `Background_Data/pyramids_kaggle_clean_manual_duration_corrected.csv` and root-level duplicate | `data/processed/final_class_specific_datasets/pyramids_kaggle_clean_manual_duration_corrected.csv` |
| `Combining_And_Manually_Correcting_Data_Files/monuments_harmonized_all.csv` | `data/processed/monuments_harmonized_all.csv` |
| `Combining_And_Manually_Correcting_Data_Files/monuments_harmonized_complete_case_positive_duration_pre1750.csv` | `data/processed/monuments_harmonized_complete_case_positive_duration_pre1750.csv` |
| harmonized manual-correction file in both the combining folder and repository root | `data/processed/monuments_harmonized_cathedral_castle_manual_duration_corrected.csv` |
| root-level manuscript figures | `figures/` |
| root-level model output CSV files | `results/` |

## 7. Running the notebooks

### Original-layout execution

The easiest way to rerun the notebooks is to recreate the original directory skeleton and then update the hard-coded absolute paths for the local machine being used.

The notebooks include both:

* hard-coded absolute paths such as:

```python
Path("/Users/jeeveshattri/Desktop/Monuments_Of_Power/Background_Data")
```

* relative paths that depend on the notebook’s working directory, such as:

```python
"../cathedral_final_researched_clean_osm_area.csv"
```

and:

```python
"monuments_harmonized_cathedral_castle_manual_duration_corrected.csv"
```

To rerun the workflow using the original structure:

1. Recreate or preserve the original folder skeleton shown in this document.
2. Place each notebook in its original directory.
3. Keep the relative positions of the required input and output files unchanged.
4. Edit any hard-coded absolute paths so that they point to the corresponding project directory on the local machine.
5. Run each notebook from the directory where it originally resided.
6. Execute the notebooks in the order listed in Section 2.

The project does not need to be stored at the exact original macOS path, provided that the hard-coded references are updated and the relative folder structure remains consistent.

### Reorganized-repository execution

The reorganized repository is intended primarily for transparent archiving and navigation. The notebooks preserve their original code and therefore are not fully path-portable without edits.

For example, when `05_analysis_and_figures.ipynb` is run from `notebooks/`, the original input:

```python
FILE_PATH = (
    "monuments_harmonized_cathedral_castle_"
    "manual_duration_corrected.csv"
)
```

would need to become:

```python
FILE_PATH = (
    "../data/processed/"
    "monuments_harmonized_cathedral_castle_manual_duration_corrected.csv"
)
```

Likewise, output paths should be redirected:

```python
OUTPUT_PATH = "../figures/feature_space.png"
```

or:

```python
SUMMARY_PATH = "../results/nonlinear_separability_nested_cv_summary.csv"
```

The same principle applies to the other notebooks.

## 8. Duplicate-file policy

The original working layout contains duplicate copies of several final datasets. These copies were retained because the notebooks referred to different locations during the original workflow.

For example:

```text
Background_Data/cathedral_final_researched_clean_osm_area.csv
cathedral_final_researched_clean_osm_area.csv
```

served different path expectations even though their contents were identical.

The original-layout worktree preserves these copies for path compatibility.

The reorganized public repository consolidates each duplicated dataset into one authoritative location under:

```text
data/processed/
```

This consolidation is organizational only. It does not represent a change to the data.

## 9. Reproducibility note

The repository provides:

- the original and enriched source data used by the pipelines;
- manual correction notes and audit trails;
- harmonized analytical datasets;
- descriptive and classification notebooks;
- manuscript figures;
- linear and nonlinear model summaries;
- fold-level nested cross-validation results;
- selected nonlinear-model parameters;
- confusion matrices;
- repeated undersampling robustness results.

The principal final modeling dataset is:

```text
data/processed/monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

The final shared features used for monument classification are:

```text
elevation_m
duration_years_harmonized
log_area_m2
```

The target variable is:

```text
monument_type
```
