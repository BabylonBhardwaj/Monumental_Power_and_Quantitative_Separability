# Monumental Power and Quantitative Separability

## Classifying Cathedrals, Castles, and Pyramids as Physical Embodiments of Authority

This repository contains the data, notebooks, manual-review records, figures, and model outputs for a digital humanities study of monumental architecture as materialized power.

The project asks whether three historically distinct monument types European cathedrals, European castles, and Egyptian pyramids—can be distinguished through measurable physical, temporal, and geographic features. The shared classification space uses:

-   elevation above sea level;
-   harmonized construction or modification duration; and
-   log-transformed base, surface, or footprint area.

The central finding is that the monument types are only partially separable with linear models but show substantially stronger nonlinear structure. Pyramids are the most quantitatively distinctive class, while cathedrals and castles overlap more strongly, reflecting both shared monumental strategies and the historical entanglement of ecclesiastical, martial, civic, territorial, and royal authority.

This repository accompanies the manuscript:

> **Monumental Power and Quantitative Separability: Classifying Cathedrals, Castles, and Pyramids as Physical Embodiments of Authority**

**Authors:** Jeevesh Attri and Pascal Wallisch\
**Affiliation:** Center for Data Science, Courant Institute of Mathematical Sciences, New York University

## Main results

The final complete-case modeling dataset contains **383 monuments**:

| Monument type | Count |
|---------------|------:|
| Cathedrals    |   268 |
| Castles       |    72 |
| Pyramids      |    43 |

Because the classes are imbalanced, model comparison emphasizes balanced accuracy and macro F1 in addition to raw accuracy.

### Linear separability

The linear models show meaningful but incomplete separability. Class weighting substantially improves performance across all three monument types, although it reduces overall accuracy by sacrificing some majority-class cathedral predictions.

| Model                               | Accuracy | Balanced accuracy |  Macro F1 |
|------------------------------|-------------:|-------------:|-------------:|
| Majority-class baseline             |    0.700 |             0.333 |     0.274 |
| Logistic regression, unweighted     |    0.723 |             0.481 |     0.472 |
| Logistic regression, class weighted |    0.601 |         **0.681** | **0.555** |
| Linear SVM, unweighted              |    0.715 |             0.412 |     0.394 |
| Linear SVM, class weighted          |    0.687 |             0.644 |     0.549 |

The strongest linear model by balanced accuracy was class-weighted logistic regression. It recalled:

-   153 of 268 cathedrals;
-   34 of 72 castles; and
-   all 43 pyramids.

Repeated undersampling checks produced balanced accuracies of approximately **0.66–0.69**, indicating that the observed linear separability was not simply an artifact of cathedral dominance.

### Nonlinear separability

Nonlinear models produced stronger balanced performance, indicating that the shared feature space contains curved boundaries, interactions, or threshold-dependent structure that linear models do not fully capture.

| Model | Accuracy | Balanced accuracy | Macro F1 |
|------------------|-----------------:|-----------------:|-----------------:|
| Majority-class baseline | 0.700 ± 0.002 | 0.333 ± 0.000 | 0.274 ± 0.001 |
| Class-weighted RBF SVM | 0.728 ± 0.048 | 0.744 ± 0.051 | 0.667 ± 0.056 |
| Class-weighted random forest | **0.773 ± 0.069** | **0.771 ± 0.077** | **0.718 ± 0.080** |
| Gradient boosting | 0.815 ± 0.047 | 0.703 ± 0.080 | 0.714 ± 0.079 |

The strongest nonlinear model by balanced accuracy was the class-weighted random forest. It recalled:

-   214 of 268 cathedrals;
-   42 of 72 castles; and
-   40 of 43 pyramids.

Taken together, the results show partial linear separability and stronger nonlinear separability. Pyramids form the most distinctive class, while cathedrals and castles overlap more strongly. This suggests meaningful but historically convergent forms of monumentality rather than cleanly divided architectural categories.

## Repository organization

``` text
.
├── data/
│   ├── raw/
│   ├── intermediate/
│   ├── manual_review/
│   └── processed/
├── external/
│   └── cathedral_source_reproduction_files/
├── figures/
├── notebooks/
├── results/
├── REPOSITORY_STRUCTURE.md
└── README.md
```

### Main directories

-   `data/raw/` contains the initial class-specific source datasets.
-   `data/intermediate/` contains cleaned, enriched, and partially processed pipeline outputs, together with retrieval caches.
-   `data/manual_review/` contains chronology-correction notes and audit trails.
-   `data/processed/` contains the final class-specific and harmonized analytical datasets.
-   `external/` contains the original cathedral reproduction package and its accompanying scripts, figures, tables, and documentation.
-   `figures/` contains the final manuscript figures.
-   `notebooks/` contains the five main notebooks in workflow order.
-   `results/` contains exported linear and nonlinear model outputs.

For the full original and reorganized trees, exact file mappings, notebook-specific input/output requirements, and path notes, see [`REPOSITORY_STRUCTURE.md`](REPOSITORY_STRUCTURE.md).

## Notebook workflow

The notebooks are numbered in their intended order:

``` text
notebooks/
├── 01_cathedral_pipeline.ipynb
├── 02_castle_pipeline.ipynb
├── 03_pyramid_pipeline.ipynb
├── 04_harmonization_and_manual_review.ipynb
└── 05_analysis_and_figures.ipynb
```

### 1. Cathedral pipeline

`01_cathedral_pipeline.ipynb`

Builds the cathedral dataset from the openICPSR church-building reproduction files, then enriches and validates records using structured and manually reviewed information. The pipeline includes:

-   cathedral filtering and identifier cleaning;
-   Wikidata and Wikipedia enrichment;
-   construction chronology review;
-   elevation lookup;
-   OpenStreetMap area enrichment;
-   style and historical-period processing; and
-   audit-file generation.

Final class-specific output:

``` text
data/processed/final_class_specific_datasets/
└── cathedral_final_researched_clean_osm_area.csv
```

### 2. Castle pipeline

`02_castle_pipeline.ipynb`

Constructs the castle dataset from a broad Wikidata retrieval and subsequent filtering, chronology reconciliation, manual review, and geographic enrichment. The pipeline includes:

-   SPARQL-based candidate retrieval;
-   castle-type filtering;
-   usable-duration filtering;
-   Wikipedia and historical-source enrichment;
-   manual duration correction;
-   OpenStreetMap footprint estimation; and
-   elevation enrichment.

Final class-specific output:

``` text
data/processed/final_class_specific_datasets/
└── european_castles_osm_area_elevation_enriched.csv
```

### 3. Pyramid pipeline

`03_pyramid_pipeline.ipynb`

Uses a fixed dataset of 62 Egyptian pyramids as its backbone and enriches it with structured identifiers, chronology, elevation, construction-status information, and manually reviewed duration evidence. The pipeline includes:

-   historical-period assignment;
-   coordinate and elevation enrichment;
-   direct-duration and reign-window evidence;
-   status classification for unfinished, abandoned, uncertain, or ruined monuments;
-   physical-dimension cleaning; and
-   manual duration correction.

Final class-specific output:

``` text
data/processed/final_class_specific_datasets/
└── pyramids_kaggle_clean_manual_duration_corrected.csv
```

### 4. Harmonization and manual review

`04_harmonization_and_manual_review.ipynb`

Combines the three final class-specific datasets into a shared analytical structure. It:

-   standardizes monument labels and classes;
-   harmonizes duration, elevation, and area variables;
-   applies documented cathedral and castle chronology corrections;
-   records applied, dropped, unmatched, and nonnumeric review decisions;
-   removes unresolved or historically incompatible cases; and
-   produces the final harmonized datasets.

Principal output:

``` text
data/processed/
└── monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

### 5. Analysis and figures

`05_analysis_and_figures.ipynb`

Produces the descriptive comparisons, figures, linear classification analyses, repeated undersampling checks, nonlinear nested cross-validation, confusion matrices, and exported result tables.

## Final analytical dataset

The principal final modeling file is:

``` text
data/processed/
└── monuments_harmonized_cathedral_castle_manual_duration_corrected.csv
```

The final shared features are:

``` text
elevation_m
duration_years_harmonized
log_area_m2
```

The target is:

``` text
monument_type
```

Area is log-transformed because raw base, surface, and footprint measurements vary substantially in scale.

The variables are comparable but not identical in historical meaning:

-   cathedral duration may represent a multigenerational institutional building span;
-   castle duration may include major fortification, rebuilding, or modification phases;
-   pyramid duration often relies on reign-window evidence and should frequently be read as an upper-bound proxy;
-   elevation carries different historical meanings across defensive, urban-ecclesiastical, and sacred-landscape settings; and
-   area is a harmonized spatial proxy rather than a perfectly uniform architectural measurement.

These limitations are treated as part of the historical-data problem rather than hidden through artificial standardization.

## Figures

The final manuscript figures are stored in `figures/`:

``` text
figures/
├── construction_duration.png
├── elevation.png
├── feature_space.png
└── log_area.png
```

They show:

-   construction-duration patterns across monument types and time;
-   elevation patterns across monument types and time;
-   log-transformed base or footprint area; and
-   the three-dimensional and pairwise distributions of monuments in the shared feature space.

## Model outputs

The `results/` directory contains the exported outputs used to report and verify the classification analyses.

### Linear-model and robustness outputs

``` text
results/
├── separability_oneoff_results_summary.csv
├── separability_repeated_undersampling_30_runs_raw.csv
└── separability_repeated_undersampling_30_runs_summary.csv
```

These include:

-   majority-class baseline performance;
-   multinomial logistic-regression performance;
-   linear SVM performance;
-   class-weighted and unweighted comparisons; and
-   repeated undersampling checks across 30 runs.

### Nonlinear nested-cross-validation outputs

``` text
results/
├── nonlinear_separability_nested_cv_summary.csv
├── nonlinear_separability_outer_fold_scores.csv
├── nonlinear_separability_selected_parameters.csv
└── nonlinear_separability_confusion_matrices.csv
```

These contain:

-   mean outer-fold scores and standard deviations;
-   fold-level accuracy, balanced accuracy, and macro F1;
-   selected inner-cross-validation hyperparameters; and
-   nested out-of-fold confusion matrices.

The nonlinear models are:

-   class-weighted RBF-kernel SVM;
-   class-weighted random forest; and
-   gradient boosting.

The outer five-fold cross-validation estimates generalization performance, while an inner three-fold cross-validation selects hyperparameters using balanced accuracy.

## Reproducing the workflow

### Recommended approach

The notebooks preserve the paths used during the original analysis. The easiest way to rerun them is to recreate the original directory skeleton and then update the hard-coded absolute paths for the local machine being used.

The code contains both hard-coded paths, such as:

``` python
Path("/Users/jeeveshattri/Desktop/Monuments_Of_Power/Background_Data")
```

and relative references, such as:

``` python
"../cathedral_final_researched_clean_osm_area.csv"
```

or:

``` python
"monuments_harmonized_cathedral_castle_manual_duration_corrected.csv"
```

To rerun the original workflow:

1.  Recreate or preserve the original folder skeleton documented in [`REPOSITORY_STRUCTURE.md`](REPOSITORY_STRUCTURE.md).
2.  Place each notebook in its original directory.
3.  Keep the relative positions of required inputs and outputs unchanged.
4.  Edit hard-coded absolute paths to point to the corresponding project directory on the local machine.
5.  Run each notebook from the directory where it originally resided.
6.  Execute the notebooks in numerical order.

The project does not need to use the original macOS path, provided the hard-coded references are changed and the relative directory skeleton remains consistent.

### Running from the reorganized structure

The reorganized repository is optimized for navigation and provenance, not automatic path portability. Running the notebooks directly from `notebooks/` requires changing their paths to the corresponding locations under:

``` text
../data/
../external/
../figures/
../results/
```

For example:

``` python
FILE_PATH = (
    "../data/processed/"
    "monuments_harmonized_cathedral_castle_manual_duration_corrected.csv"
)
```

See [`REPOSITORY_STRUCTURE.md`](REPOSITORY_STRUCTURE.md) for every original path and its current equivalent.

## Software

The main analysis is implemented in Python notebooks. Principal packages used across the workflow include:

``` text
pandas
numpy
matplotlib
scikit-learn
requests
beautifulsoup4
openpyxl
```

Additional geospatial, parsing, or networking dependencies may be used by individual enrichment cells. The original cathedral reproduction package also contains R scripts and its own documentation under:

``` text
external/cathedral_source_reproduction_files/
```

For exact imports, consult the first cells of each notebook.

------------------------------------------------------------------------

## Data provenance and manual review

The three monument datasets required different curation strategies:

-   **Cathedrals:** an existing research dataset was filtered, enriched, and manually reviewed.
-   **Castles:** a new dataset was assembled from broad Wikidata retrieval and supplementary sources.
-   **Pyramids:** a fixed public dataset was enriched and manually reviewed, particularly for uncertain construction chronology.

Manual-review materials are preserved in:

``` text
data/manual_review/
├── notes/
└── audits/
```

These files document:

-   historical chronology decisions;
-   corrections applied to cathedral and castle records;
-   records removed from analysis;
-   unmatched correction notes; and
-   records retained without numerical alteration.

The project intentionally preserves this audit trail because historical-data curation is part of the scholarly analysis.

## External source material

The directory:

``` text
external/cathedral_source_reproduction_files/
```

contains the third-party reproduction package associated with prior research on European church construction. It includes source data, R scripts, figures, tables, documentation, and licensing information.

External data and materials retain their original attribution, licensing, and terms of use. Any license applied to this repository’s original code does not automatically supersede third-party data licenses.

## Interpretation

The models are used as instruments of historical interpretation rather than replacements for it.

The results suggest:

-   pyramids form the most distinctive physical-temporal cluster;
-   cathedrals and castles overlap strongly because both emerged from long-lived and mutable systems of medieval authority;
-   nonlinear models recover meaningful structure that linear boundaries miss; and
-   confusion between monument types is itself historically informative.

The broader argument is that monumental architecture turns abstract authority into scale, duration, spatial occupation, visibility, and durable presence. Cathedrals, castles, and pyramids were historically different, but all used built form to make power materially and psychologically legible.

## Key data sources and references

The repository draws on publicly available datasets and prior scholarship on
monumental architecture, historical construction, landscape, and digital
humanities. The full bibliography appears in the accompanying manuscript.

### Principal datasets

- Buringh, E., Campbell, B. M., Rijpma, A., and van Zanden, J. L. (2020).
  “Church Building and the Economy during Europe’s ‘Age of the Cathedrals’,
  700–1500 CE.” *Explorations in Economic History*, 76, 101316.

- Rijpma, A., Buringh, E., and van Zanden, J. L. (2019).
  *Church Building in Western Europe, 700–1500 CE* [Data set]. openICPSR.

- Chemkaeva, D. (2019).
  *OpenStreetMap of Pyramids of Ancient Egypt* [Dataset and code repository].
  GitHub.

### Monumentality and digital humanities

- Münster, S., and Terras, M. (2020).
  “The Visual Side of Digital Humanities: A Survey on Topics, Researchers,
  and Epistemic Cultures.” *Digital Scholarship in the Humanities*, 35(2),
  366–389.

- Osborne, J. F. (Ed.). (2014).
  *Approaching Monumentality in Archaeology*. State University of New York
  Press.

- Trigger, B. G. (1990).
  “Monumental Architecture: A Thermodynamic Explanation of Symbolic
  Behaviour.” *World Archaeology*, 22(2), 119–132.

- Stanish, C., Earle, T., García Sanjuán, L., Tantaleán, H., and Barrientos, G.
  (2024). “Early Monumentality, Ritual, and Political Complexity: Formative
  Peru and Copper Age Iberia.” *Current Anthropology*, 65(5), 810–836.

### Spatial and architectural context

- Oulmas, M., Abdessemed-Foufa, A., Avilés, A. B. G., and Conesa, J. I. P.
  (2023). “Assessing the Defensibility of Medieval Fortresses on the
  Mediterranean Coast.” *ISPRS International Journal of Geo-Information*,
  13(1), 2.

- Magli, G. (2009).
  “Geometry and Perspective in the Landscape of the Saqqara Pyramids.”
  arXiv.

- Magli, G. (2010).
  *Architecture, Astronomy and Sacred Landscape in Ancient Egypt*.
  Cambridge University Press.

- Lehner, M. (1997).
  *The Complete Pyramids*. Thames & Hudson.

- Verner, M. (2001).
  *The Pyramids: Their Archaeology and History*. Atlantic Books.

### Castle history and chronology

- Brown, R. A. (1962). *English Castles*. B. T. Batsford.
- Pounds, N. J. G. (1994). *The Medieval Castle in England and Wales*.
  Cambridge University Press.
- Creighton, O. H. (2005). *Castles and Landscapes*. Equinox.
- Liddiard, R. (2005). *Castles in Context*. Windgather Press.

## Authors

**Jeevesh Attri**\
Data curation, formal analysis, investigation, validation, visualization, and original drafting

**Pascal Wallisch**\
Conceptualization, methodology, supervision, review, and editing

Center for Data Science\
Courant Institute of Mathematical Sciences\
New York University

## Citation

The manuscript is currently being prepared for submission. A formal citation and persistent identifier will be added when available.

Until then, please cite the repository and manuscript title together with the authors:

``` text
Jeevesh Attri and Pascal Wallisch.
“Monumental Power and Quantitative Separability: Classifying Cathedrals,
Castles, and Pyramids as Physical Embodiments of Authority.”
Research code and data repository.
```
