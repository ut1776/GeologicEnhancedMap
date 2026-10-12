# Geologic Enhanced Mapping System (GEMS)

### Machine Learning, Geophysical Data Integration, and Distance-Weighted Mineral Prospectivity Mapping

GEMS (Geologic Enhanced Mapping System) is a geospatial machine-learning framework designed to integrate geophysical predictors, generate mineral prospectivity maps, characterize spatial prediction patterns, and prioritize high-prospectivity exploration targets.

The project combines raster-based predictor integration, machine-learning inference, geospatial visualization, feature analysis, and distance-weighted evaluation into a reproducible workflow. Its outputs are intended to support geological interpretation and exploration planning, not replace field validation or establish the presence of an economic mineral deposit.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Project Objectives](#2-project-objectives)
3. [Study Grid and Data Characteristics](#3-study-grid-and-data-characteristics)
4. [System Architecture](#4-system-architecture)
5. [Workflow](#5-workflow)
6. [Prediction Results](#6-prediction-results)
7. [Feature and Geophysical Analysis](#7-feature-and-geophysical-analysis)
8. [Exploration Target Prioritization](#8-exploration-target-prioritization)
9. [Distance-Weighted Tversky Evaluation](#9-distance-weighted-tversky-evaluation)
10. [Figures](#10-figures)
11. [Data Tables](#11-data-tables)
12. [Repository Structure](#12-repository-structure)
13. [Reproducibility](#13-reproducibility)
14. [Limitations and Future Work](#14-limitations-and-future-work)
15. [Conclusion](#15-conclusion)
16. [Citation](#16-citation)

---

## 1. Project Overview

Mineral prospectivity mapping attempts to identify locations whose geological and geophysical characteristics are consistent with known or hypothesized mineralization patterns.

GEMS approaches this task as a spatial prediction and exploration-prioritization problem. The framework integrates geophysical raster predictors and derived features to produce a continuous prospectivity surface. It then summarizes the predicted spatial distribution, analyzes feature characteristics, and identifies high-priority candidate locations.

The archived project reports the following principal characteristics:

| Characteristic              | Reported value |
| --------------------------- | -------------: |
| Number of predictors        |             43 |
| Base geophysical bands      |             20 |
| Nominal raster resolution   |          100 m |
| Raster width                |   3,292 pixels |
| Raster height               |   3,730 pixels |
| Coordinate reference system |     EPSG:32611 |
| Finite prediction pixels    |      4,733,111 |
| Finite-pixel coverage       |         38.55% |

The reported coverage is the fraction of the nominal raster grid containing finite predictions. It should not be interpreted as the percentage of the study area containing mineralization.

## 2. Project Objectives

GEMS is designed to:

* Integrate multiple geophysical and derived predictors into a consistent modeling workflow.
* Generate spatially continuous prospectivity predictions wherever the required inputs support inference.
* Visualize prospectivity in relation to geophysical signatures and spatial context.
* Summarize predictor statistics and model performance.
* Rank candidate exploration targets for further geological investigation.
* Examine spatial tolerance and distance-weighted evaluation concepts.
* Preserve figures, tabular outputs, and analysis summaries in a repository suitable for review and further development.

The intended output is a decision-support layer for exploration screening rather than a definitive mineral-resource assessment.

## 3. Study Grid and Data Characteristics

The archived prediction grid has a nominal cell size of 100 m and uses **EPSG:32611**, a projected coordinate reference system based on WGS 84 / UTM zone 11N.

The raster dimensions are 3,292 columns by 3,730 rows. Not every grid cell contains a finite prediction, so the valid-data footprint is smaller than the full rectangular grid.

The workflow uses 43 predictors, including 20 base geophysical bands and additional derived or processed features.

### Data interpretation

The input layers provide spatially varying information that may help distinguish locations with different geophysical signatures. The resulting prediction surface represents model-estimated prospectivity under the assumptions and limitations of the underlying data and training procedure.

Before reproducing the analysis, users should verify that all input rasters share a compatible spatial reference, grid alignment, resolution, and NoData convention.

## 4. System Architecture

The GEMS workflow can be summarized as follows:

1. **Input inventory:** identify the selected input files and available predictor layers.
2. **Spatial preparation:** prepare the raster predictors on the target grid and account for missing values.
3. **Feature integration:** assemble the predictor variables used by the model.
4. **Model inference:** produce prospectivity predictions from the available inputs.
5. **Spatial analysis:** examine prediction distributions, geophysical signatures, and mapped spatial patterns.
6. **Target prioritization:** rank high-prospectivity cells or spatial targets.
7. **Evaluation:** summarize available performance measures and distance-weighted diagnostics.
8. **Artifact generation:** export maps, tables, and summaries for inspection and reproducibility.

The precise implementation details of model training, calibration, and preprocessing should be established from the corresponding scripts, configuration files, and archived model artifacts before attempting an independent reproduction.

## 5. Workflow

### 5.1 Input preparation

The workflow inventories the selected input files and predictor layers. Raster preparation must preserve consistent spatial alignment so that each modeled cell refers to the same geographic location across predictors.

### 5.2 Predictor integration

The 43-predictor feature set combines base geophysical information with additional features. The feature-statistics table provides a starting point for reviewing predictor distributions and identifying variables that may require further quality control.

### 5.3 Prospectivity prediction

The model produces a continuous prediction surface. The values are useful for relative spatial prioritization, subject to the model's calibration, training labels, and the validity of its input layers.

A high prediction value should not automatically be interpreted as a probability of discovering an economic deposit unless that probabilistic interpretation has been independently validated.

### 5.4 Spatial visualization

The generated maps show the relationship between prediction values, geographic context, selected geophysical signatures, and derived spatial indicators.

### 5.5 Target ranking

Candidate cells are ranked using the archived prospectivity outputs. The top-target table provides a structured starting point for geological review and additional investigation.

### 5.6 Evaluation and reporting

Performance summaries and distance-weighted diagnostics are preserved as CSV files. These records should be interpreted according to their documented definitions and should not be treated as interchangeable metrics.

## 6. Prediction Results

The archived prediction summary reports the following distribution:

| Statistic                | Reported value |
| ------------------------ | -------------: |
| Minimum prediction       |       0.000063 |
| Median prediction        |         0.0265 |
| Mean prediction          |         0.0672 |
| Standard deviation       |         0.1015 |
| Maximum prediction       |         0.9344 |
| Finite prediction pixels |      4,733,111 |
| Finite-pixel coverage    |         0.3855 |

These statistics indicate that the prediction surface is not uniformly distributed across its valid footprint. The mean is higher than the median, consistent with a distribution in which a subset of cells has comparatively high predictions.

This summary alone does not establish model calibration, geological correctness, or economic significance. Those interpretations require appropriate independent evidence.

### Archived model-performance metrics

The archived model-performance summary reports:

| Metric       | Reported value |
| ------------ | -------------: |
| Mean ROC-AUC |         0.6612 |
| Mean PR-AUC  |         0.0318 |

ROC-AUC and PR-AUC measure different aspects of predictive discrimination. Their interpretation depends on the validation design, the distribution of positive and negative labels, and the precise metric implementation.

In particular, PR-AUC can be strongly affected by the prevalence of positive examples. The reported values should therefore be considered alongside the evaluation dataset, class balance, and validation protocol rather than interpreted in isolation.

For the complete archived records, see [`model_performance.csv`](Tables/model_performance.csv) and [`prediction_summary.csv`](Tables/prediction_summary.csv).

### Prediction map

![GEMS prediction map](Figures/02_GEMS_prediction_map.png)

*Figure 1. GEMS prediction surface showing the spatial distribution of model-generated prospectivity values.*

## 7. Feature and Geophysical Analysis

Feature analysis helps describe the information available to the prediction system and provides context for interpreting spatial patterns.

The archived project includes feature statistics and geophysical-signature visualizations. These artifacts can be used to examine predictor ranges, identify potentially influential spatial patterns, and guide further investigation.

Feature statistics should not be confused with model feature importance. A variable's range or variability does not establish how much it contributes to a model's predictions. Feature importance claims require a documented method, such as model-specific importance, permutation importance, or an appropriate attribution analysis.

### Geophysical signatures

![GEMS geophysical signatures](Figures/03_GEMS_geophysical_signatures.png)

*Figure 2. Geophysical signatures used to characterize the predictor data and spatial context of the GEMS analysis.*

### Feature statistics

The full predictor statistics are available in [`feature_statistics.csv`](Tables/feature_statistics.csv).

### Distance-weighted spatial diagnostics

![Distance-weighted Tversky analysis](Figures/03_distance_weighted_tversky.png)

*Figure 3. Archived distance-weighted Tversky analysis.*

A corresponding heatmap is available here:

![Distance-weighted Tversky heatmap](Figures/03_distance_weighted_tversky_heatmap.png)

*Figure 4. Heatmap associated with the archived distance-weighted Tversky analysis.*

The interpretation of these diagnostics depends on the exact definitions of the positive, false-positive, and false-negative contributions and the spatial weighting procedure.

## 8. Exploration Target Prioritization

GEMS ranks high-prospectivity cells to support subsequent geological review. Target prioritization helps convert a large raster surface into a more manageable list of locations for inspection.

The archived project includes a top-target visualization and a CSV containing up to 100 ranked prospectivity targets.

![Top prospectivity targets](Figures/07_top_prospectivity_targets.png)

*Figure 5. Highest-ranked prospectivity targets in the archived GEMS analysis.*

The associated table is [`top_100_prospectivity_targets.csv`](Tables/top_100_prospectivity_targets.csv).

Target rankings are model-dependent. Before using them to direct field work, users should consider geological context, data quality, spatial clustering, access constraints, and the possibility that several high-ranked cells represent a single spatially continuous target rather than independent prospects.

### Prospectivity overlay

![Satellite prospectivity overlay](Figures/01_satellite_prospectivity_overlay.png)

*Figure 6. Prospectivity predictions displayed with satellite or geographic context.*

This overlay supports visual inspection of spatial relationships. It does not, by itself, demonstrate that predicted targets correspond to verified mineral occurrences.

## 9. Distance-Weighted Tversky Evaluation

The conventional Tversky index is defined as:

$$
T_{\alpha,\beta}
=
\frac{TP}{TP+\alpha FP+\beta FN}
$$

where:

* \(TP\) represents the true-positive contribution.
* \(FP\) represents the false-positive contribution.
* \(FN\) represents the false-negative contribution.
* \(\alpha\) controls the penalty associated with false positives.
* \(\beta\) controls the penalty associated with false negatives.

The archived GEMS portfolio reports a spatial tolerance of **300 m**, equivalent to three nominal 100 m pixels, with:

$$
\alpha = 0.2,\qquad \beta = 0.8
$$

The distance-weighted implementation modifies contributions according to spatial proximity. This allows spatial offsets to be considered rather than treating every prediction-reference mismatch identically.

### Archived distance-weighted results

The project records multiple distance-weighted diagnostics:

| Diagnostic                                   | Reported value |
| -------------------------------------------- | -------------: |
| Mean probabilistic distance-weighted Tversky |         0.0616 |
| Mean best hard distance-weighted Tversky     |         0.1148 |
| Separate archived summary score              |         0.2502 |
| Archived \(TP_w\) contribution               |      26,283.97 |
| Archived \(FP_w\) contribution               |     255,000.52 |
| Archived \(FN_w\) contribution               |      34,704.00 |

The first two values summarize the probabilistic and best-hard diagnostics, respectively. The value 0.2502 belongs to a separate archived summary and should not be assumed to be the same statistic or aggregation as either mean above.

The weighted contributions \(TP_w\), \(FP_w\), and \(FN_w\) are retained as reported in the archived summary. They should be interpreted according to the implementation that generated them.

**Evaluation note:** The conventional Tversky equation is included for reference. Official competition comparisons must use the exact competition scoring implementation, including its distance-weighting, matching, tolerance, aggregation, and threshold rules. A substitute approximation must not be presented as an official score.

The related artifacts are:

* [`distance_weighted_tversky_summary.csv`](Tables/distance_weighted_tversky_summary.csv)
* [`dwt_pixel_contributions.csv`](Tables/dwt_pixel_contributions.csv)
* [`threshold_analysis.csv`](Tables/threshold_analysis.csv)

The associated visualization is [`03_distance_weighted_tversky_heatmap.png`](Figures/03_distance_weighted_tversky_heatmap.png).

## 10. Figures

The following figures are included in the repository's `Figures/` directory.

### 10.1 Executive dashboard

![GEMS executive dashboard](Figures/01_GEMS_executive_dashboard.png)

*Figure 7. Executive overview of the GEMS project and its archived outputs.*

### 10.2 Prospectivity map

![GEMS prospectivity map](Figures/02_GEMS_prospectivity_map.png)

*Figure 8. Prospectivity visualization generated by the GEMS workflow.*

### 10.3 Prospectivity and geological lines

![Prospectivity and geologic lines](Figures/02_prospectivity_geologic_lines.png)

*Figure 9. Prospectivity patterns displayed with geological line context.*

### 10.4 Distance-weighted Tversky map

![Distance-weighted Tversky map](Figures/04_distance_weighted_tversky_map.png)

*Figure 10. Spatial visualization of the archived distance-weighted Tversky analysis.*

### 10.5 DEM, hillshade, and contours

![DEM hillshade and contours](Figures/05_dem_hillshade_contours.png)

*Figure 11. Digital elevation model, hillshade, and contour visualization for geographic context.*

### 10.6 Feature signatures

![Model feature signatures](Figures/08_model_feature_signatures.png)

*Figure 12. Feature-signature visualization associated with the archived modeling analysis.*

The figure links above use repository-relative paths. GitHub renders them when the referenced image files exist at those exact paths and are committed to the repository. Filenames and capitalization must match the actual repository contents.

## 11. Data Tables

The `Tables/` directory contains CSV artifacts supporting the archived analysis.

| File                                                                                    | Purpose                                                |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| [`GEMS_portfolio_summary.csv`](Tables/GEMS_portfolio_summary.csv)                       | Portfolio-level summary of the archived analysis       |
| [`distance_weighted_tversky_summary.csv`](Tables/distance_weighted_tversky_summary.csv) | Summary of distance-weighted Tversky diagnostics       |
| [`dwt_pixel_contributions.csv`](Tables/dwt_pixel_contributions.csv)                     | Pixel-level or pixel-aggregated weighted contributions |
| [`feature_statistics.csv`](Tables/feature_statistics.csv)                               | Predictor statistics                                   |
| [`model_performance.csv`](Tables/model_performance.csv)                                 | Archived model-performance metrics                     |
| [`prediction_summary.csv`](Tables/prediction_summary.csv)                               | Summary statistics for the prediction surface          |
| [`prospectivity_cells.csv`](Tables/prospectivity_cells.csv)                             | Prospectivity-cell records                             |
| [`selected_input_files.csv`](Tables/selected_input_files.csv)                           | Inventory of selected input files                      |
| [`threshold_analysis.csv`](Tables/threshold_analysis.csv)                               | Threshold-related evaluation summaries                 |
| [`top_100_prospectivity_targets.csv`](Tables/top_100_prospectivity_targets.csv)         | Ranked high-prospectivity target records               |

These tables are provided to make the archived outputs easier to inspect and reuse. Their exact column meanings, units, and aggregation rules should be confirmed from the generating code or accompanying metadata before using them in another analysis.

## 12. Repository Structure

The principal artifact layout is:

```text
GeologicEnhancedMap/
├── README.md
├── Figures/
│   ├── 01_GEMS_executive_dashboard.png
│   ├── 01_satellite_prospectivity_overlay.png
│   ├── 02_GEMS_prediction_map.png
│   ├── 02_GEMS_prospectivity_map.png
│   ├── 02_prospectivity_geologic_lines.png
│   ├── 03_GEMS_geophysical_signatures.png
│   ├── 03_distance_weighted_tversky.png
│   ├── 03_distance_weighted_tversky_heatmap.png
│   ├── 04_distance_weighted_tversky_map.png
│   ├── 05_dem_hillshade_contours.png
│   ├── 07_top_prospectivity_targets.png
│   ├── 08_model_feature_signatures.png
│   └── .gitkeep
└── Tables/
    ├── GEMS_portfolio_summary.csv
    ├── distance_weighted_tversky_summary.csv
    ├── dwt_pixel_contributions.csv
    ├── feature_statistics.csv
    ├── model_performance.csv
    ├── prediction_summary.csv
    ├── prospectivity_cells.csv
    ├── selected_input_files.csv
    ├── threshold_analysis.csv
    ├── top_100_prospectivity_targets.csv
    └── .gitkeep
```

This tree describes the principal figure and table artifacts. Additional scripts, configuration files, source data, or model files may exist elsewhere in the repository.

## 13. Reproducibility

For a reproducible rerun or independent review:

1. Clone or download the repository.
2. Inspect the available source code and document the software environment.
3. Verify the provenance and licensing of input data.
4. Confirm raster coordinate systems, resolution, grid alignment, and NoData handling.
5. Identify the exact predictor list and preprocessing procedure.
6. Verify the trained model or training configuration used to generate predictions.
7. Reproduce the prediction surface before comparing derived summaries.
8. Validate metric definitions and aggregation rules against the archived evaluation implementation.
9. Compare regenerated CSVs and figures with the archived outputs.

The figures and tables in this repository document the archived results. Their presence alone does not guarantee that the entire pipeline can be reproduced without the original source datasets, model artifacts, dependencies, and configuration.

## 14. Limitations and Future Work

### 14.1 Data coverage

Only 38.55% of the nominal prediction grid contains finite predictions in the archived summary. The reasons for missing coverage should be investigated, including source-data footprints, missing predictors, preprocessing filters, and masking rules.

### 14.2 Validation and label quality

The reliability of prospectivity predictions depends on the quality and completeness of known mineral occurrences, reference targets, negative examples, and other labels used during training or evaluation.

Incomplete or spatially biased labels can cause apparent model performance to differ from real-world exploration performance.

### 14.3 Spatial leakage

Randomly splitting nearby spatial observations between training and evaluation can overestimate generalization. Future assessments should consider spatially separated validation, geographically independent test regions, and sensitivity to the sampling strategy.

### 14.4 Metric consistency

ROC-AUC, PR-AUC, conventional Tversky, probabilistic distance-weighted Tversky, and hard distance-weighted Tversky represent different evaluation concepts. Comparisons require consistent definitions, thresholds, weighting, and aggregation.

The archived distance-weighted summaries should be reconciled with the exact implementation before they are reported as official benchmark results.

### 14.5 Geological interpretation

Geophysical similarity and high model scores do not establish mineralization, grade, tonnage, recoverability, or economic viability. Candidate targets require independent geological assessment and, where appropriate, field investigation.

### 14.6 Recommended future improvements

Potential next steps include:

* Documenting the complete predictor lineage and preprocessing configuration.
* Adding explicit data-quality and spatial-coverage diagnostics.
* Establishing geographically independent validation.
* Evaluating sensitivity to label uncertainty and threshold selection.
* Recording model calibration and uncertainty where appropriate.
* Documenting the precise distance-weighted scoring implementation.
* Comparing model-ranked targets with independent geological evidence.
* Adding automated checks that verify every referenced figure and table exists before publishing the README.

## 15. Conclusion

GEMS provides an integrated framework for geophysical predictor analysis, spatial prospectivity prediction, exploration-target ranking, and distance-weighted evaluation diagnostics.

The archived outputs include a 100 m prediction grid, predictor statistics, model-performance summaries, target rankings, and a collection of visualizations and CSV artifacts. Together, these materials support review of the prediction patterns and provide a basis for further validation and development.

The most important next step is to establish reproducible provenance for the input layers, model, validation protocol, and distance-weighted scoring implementation. These details are necessary to assess how reliably the archived predictions generalize to new exploration areas.

## 16. Citation

If you use or adapt GEMS, cite the repository and the associated data sources and model implementation used in your work.

**Repository:** [GeologicEnhancedMap — GitHub](https://github.com/ut1776/GeologicEnhancedMap)

**Suggested citation format:**

> Tabbsum, U. *Geologic Enhanced Mapping System (GEMS): Machine Learning, Geophysical Data Integration, and Distance-Weighted Mineral Prospectivity Mapping.* GitHub repository: https://github.com/ut1776/GeologicEnhancedMap.

Please verify the preferred author attribution, publication year, and any formal publication details before using this as a final bibliographic citation.

---

*Disclaimer: GEMS is a research and exploration-support framework. Predictions and ranked targets are not proof of mineral deposits or economic viability. Users should verify data provenance, licensing, evaluation methodology, and geological evidence before making operational decisions.*
