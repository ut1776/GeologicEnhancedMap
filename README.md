# Geologic Enhanced Mapping System (GEMS)

### AI-Assisted Fault Mapping | Geospatial Machine Learning | Geothermal Exploration

<p align="center">
  <img src="Figures/01_GEMS_executive_dashboard.png" alt="GEMS executive dashboard" width="100%">
</p>

<p align="center">
  <strong>Integrating terrain, geophysical evidence, and machine learning to prioritize geological structures.</strong>
</p>

<p align="center">
  <a href="https://github.com/ut1776/GeologicEnhancedMap">
    <img src="https://img.shields.io/badge/Repository-GeologicEnhancedMap-176B87?style=for-the-badge&logo=github&logoColor=white" alt="GitHub repository">
  </a>
  <img src="https://img.shields.io/badge/Model-LightGBM-27864B?style=for-the-badge" alt="LightGBM">
  <img src="https://img.shields.io/badge/Domain-Geospatial%20AI-7057A3?style=for-the-badge" alt="Geospatial AI">
  <img src="https://img.shields.io/badge/Focus-Geothermal%20Exploration-D98B25?style=for-the-badge" alt="Geothermal exploration">
</p>

**Geologic Enhanced Mapping System (GEMS)** is an independent geospatial machine-learning research portfolio investigating how geophysical measurements, terrain derivatives, and contextual spatial features can help identify and prioritize potential geological fault structures across Nevada and adjacent eastern California.

The project combines a reported 43-feature modeling pipeline with LightGBM, spatial prediction maps, distance-weighted evaluation diagnostics, and ranked prospectivity records.

Its objective is to support geological interpretation by directing attention toward locations that may warrant further investigation.

> **Core principle:** A model-generated prospectivity score is a geological hypothesis, not proof of a fault or a productive geothermal reservoir.

---

## Contents

* [1. Project overview](#1-project-overview)
* [2. Executive dashboard](#2-executive-dashboard)
* [3. Regional prediction maps](#3-regional-prediction-maps)
* [4. Terrain and DEM analysis](#4-terrain-and-dem-analysis)
* [5. Geophysical evidence](#5-geophysical-evidence)
* [6. Model diagnostics](#6-model-diagnostics)
* [7. Data and results](#7-data-and-results)
* [8. Methodology](#8-methodology)
* [9. Distance-weighted Tversky evaluation](#9-distance-weighted-tversky-evaluation)
* [10. Reproducibility and validation](#10-reproducibility-and-validation)
* [11. Repository structure](#11-repository-structure)
* [12. Research roadmap](#12-research-roadmap)
* [13. Limitations](#13-limitations)
* [14. References](#14-references)
* [15. Acknowledgements](#15-acknowledgements)

---

## 1. Project overview

Geothermal systems depend on a favorable combination of heat, fluid, and permeability. Geological faults may facilitate fluid circulation, redirect flow, or act as barriers depending on their structural and geological characteristics.

However, existing fault inventories are incomplete. Structures may be concealed beneath sediments, poorly expressed at the surface, or omitted from earlier maps. Conversely, drainage, roads, erosional boundaries, and lithological contacts can resemble geological lineaments.

GEMS explores whether combining multiple imperfect evidence sources can improve the prioritization of potential fault locations.

### Research objectives

| Objective                            | Approach                                                                                 |
| ------------------------------------ | ---------------------------------------------------------------------------------------- |
| Integrate spatial evidence           | Combine base geophysical bands with derived and contextual predictors                    |
| Identify fault-associated patterns   | Use LightGBM gradient-boosted decision trees                                             |
| Generate continuous spatial rankings | Produce prospectivity score surfaces                                                     |
| Evaluate prediction behavior         | Examine ROC-AUC, PR-AUC, and distance-weighted Tversky diagnostics                       |
| Support geological review            | Visualize predictions alongside terrain, geological linework, and geophysical signatures |
| Preserve research artifacts          | Maintain figures, CSV summaries, threshold diagnostics, and ranked targets               |

### Intended application

The primary application is decision support for geological fault mapping and geothermal exploration. The workflow may also provide a foundation for other geoscience mapping problems involving incomplete labels and heterogeneous spatial datasets.

This repository documents an archived research portfolio. The reported metrics are not presented as independently verified official competition results.

---

## 2. Executive dashboard

The following values are reported in the archived project summaries.

| Indicator                   | Reported value |
| --------------------------- | -------------: |
| Model                       |       LightGBM |
| Total predictors            |             43 |
| Base geophysical bands      |             20 |
| Raster width                |    3,292 cells |
| Raster height               |    3,730 cells |
| Nominal pixel size          |          100 m |
| Coordinate reference system |     EPSG:32611 |
| Finite prediction pixels    |      4,733,111 |
| Finite prediction coverage  |         38.55% |
| Mean ROC-AUC                |         0.6612 |
| Mean PR-AUC                 |         0.0318 |
| Mean probabilistic DWT      |         0.0616 |
| Mean best hard DWT          |         0.1148 |
| Separately reported DWT     |         0.2502 |

Source files:

* [`GEMS_portfolio_summary.csv`](Tables/GEMS_portfolio_summary.csv)
* [`prediction_summary.csv`](Tables/prediction_summary.csv)
* [`model_performance.csv`](Tables/model_performance.csv)
* [`distance_weighted_tversky_summary.csv`](Tables/distance_weighted_tversky_summary.csv)

### Interpretation

* **43 predictors:** The reported model integrates multiple base and derived feature types.
* **100 m nominal grid:** The output grid is fine-resolution, but the effective resolution depends on the original data sources.
* **38.55% coverage:** Only part of the recorded grid contains finite predictions. Uncovered cells must not be interpreted as low prospectivity.
* **ROC-AUC of 0.6612:** This is the recorded mean discrimination metric under the archived evaluation design.
* **PR-AUC of 0.0318:** Interpretation depends on positive-label prevalence, sampling design, and the completeness of the fault inventory.
* **Multiple DWT values:** The probabilistic, hard-threshold, and separate weighted-contribution summaries describe distinct recorded calculations and must not be conflated.

These values establish a baseline for further investigation, not proof of successful discovery of previously unmapped faults.

---

## 3. Regional prediction maps

### 3.1 Executive overview

![GEMS executive dashboard](Figures/01_GEMS_executive_dashboard.png)

*Figure 1. Executive dashboard summarizing the GEMS mapping portfolio.*

[Open the executive dashboard](Figures/01_GEMS_executive_dashboard.png)

### 3.2 Regional prediction surface

![GEMS regional prediction map](Figures/02_GEMS_prediction_map.png)

*Figure 2. Regional prediction surface for the study grid.*

[Open the regional prediction map](Figures/02_GEMS_prediction_map.png)

### 3.3 Prospectivity score surface

![GEMS prospectivity map](Figures/02_GEMS_prospectivity_map.png)

*Figure 3. Continuous model scores used to prioritize locations for geological review.*

[Open the prospectivity map](Figures/02_GEMS_prospectivity_map.png)

Higher scores indicate stronger similarity to patterns learned from the training labels. They should not automatically be interpreted as calibrated probabilities of fault existence.

### 3.4 Geological linework overlay

![Prospectivity with geological linework](Figures/02_prospectivity_geologic_lines.png)

*Figure 4. Comparison of prospectivity scores and geological linework.*

[Open the geological linework overlay](Figures/02_prospectivity_geologic_lines.png)

Comparing predicted patterns with existing geological linework helps identify agreement, potential extensions, and locations that require further interpretation.

### 3.5 Satellite-context overlay

![Satellite prospectivity overlay](Figures/01_satellite_prospectivity_overlay.png)

*Figure 5. Prospectivity predictions displayed in landscape context.*

[Open the satellite-context overlay](Figures/01_satellite_prospectivity_overlay.png)

Satellite imagery can help reviewers investigate possible terrain expressions and distinguish geological hypotheses from roads, drainage, and other non-tectonic features. Its display here does not establish that satellite imagery was used as a model input.

### 3.6 Ranked targets

![Top prospectivity targets](Figures/07_top_prospectivity_targets.png)

*Figure 6. High-ranking prospectivity targets for follow-up investigation.*

[Open the ranked-target figure](Figures/07_top_prospectivity_targets.png)

Candidate ranking is a prioritization mechanism. Geological confirmation requires independent evidence and, where feasible, additional mapping or field investigation.

---

## 4. Terrain and DEM analysis

Digital elevation models provide geomorphic context for interpreting potential structural features. Fault-related surface expressions may include scarps, aligned valleys, slope breaks, linear ridges, and drainage offsets.

These landforms are not unique to faulting. Their interpretation depends on geomorphology, lithology, erosion, DEM resolution, and independent geological evidence.

![DEM hillshade and contours](Figures/05_dem_hillshade_contours.png)

*Figure 7. DEM hillshade and contour visualization for terrain and lineament inspection.*

[Open the DEM analysis figure](Figures/05_dem_hillshade_contours.png)

### Terrain evidence

| Feature      | Potential value                                    | Limitation                                         |
| ------------ | -------------------------------------------------- | -------------------------------------------------- |
| Hillshade    | Reveals terrain breaks and aligned landforms       | Depends on illumination direction                  |
| Slope        | Highlights abrupt terrain transitions              | Can emphasize erosional or lithological boundaries |
| Curvature    | Describes changes in terrain shape                 | Sensitive to noise and cell size                   |
| Local relief | Measures neighborhood elevation contrasts          | Depends on neighborhood scale                      |
| Contours     | Reveals changes in elevation and landform geometry | Does not directly establish subsurface faulting    |

### Why combine terrain and geophysics?

Topography describes the surface, while geophysical products provide indirect evidence about subsurface physical-property contrasts.

A buried structure may have a geophysical signature without a strong terrain expression. Conversely, a prominent valley may be erosional rather than tectonic.

The strongest interpretation comes from evaluating the consistency of independent evidence sources.

---

## 5. Geophysical evidence

The archived feature inventory records 20 base geophysical bands and 43 total predictors.

The report describes feature categories that include magnetic and gravity products and derivatives, radiometric or related variables, deformation-rate information, conductivity, depth-to-basement-related information, and elevation.

The precise meaning, units, source, and processing history of each feature should be verified against the original data inventory.

![GEMS geophysical signatures](Figures/03_GEMS_geophysical_signatures.png)

*Figure 8. Geophysical signatures associated with the model's high-ranking predictions.*

[Open the geophysical-signatures figure](Figures/03_GEMS_geophysical_signatures.png)

### Evidence interpretation

* **Magnetic products:** May reveal contrasts in magnetic properties and potential structural boundaries.
* **Gravity products:** May highlight density contrasts and regional subsurface structure.
* **Geophysical derivatives:** Can emphasize local gradients and boundaries but may amplify noise.
* **Conductivity-related information:** May provide complementary evidence about subsurface electrical properties.
* **Elevation and terrain features:** Describe surface morphology and possible geomorphic expression.
* **Contextual predictors:** Can help the model combine local evidence across multiple spatial scales.

None of these features is uniquely diagnostic of a fault. Their value depends on geological context, data quality, and the consistency of multiple observations.

---

## 6. Model diagnostics

GEMS includes archived diagnostic figures for evaluating spatial agreement, distance-weighted scores, and model feature behavior.

### 6.1 Distance-weighted Tversky diagnostics

![Distance-weighted Tversky diagnostics](Figures/03_distance_weighted_tversky.png)

*Figure 9. Archived distance-weighted Tversky evaluation diagnostics.*

[Open the diagnostic figure](Figures/03_distance_weighted_tversky.png)

### 6.2 Spatial evaluation heatmap

![Distance-weighted Tversky heatmap](Figures/03_distance_weighted_tversky_heatmap.png)

*Figure 10. Spatial visualization of distance-weighted evaluation contributions.*

[Open the evaluation heatmap](Figures/03_distance_weighted_tversky_heatmap.png)

### 6.3 Spatial evaluation map

![Distance-weighted Tversky spatial map](Figures/04_distance_weighted_tversky_map.png)

*Figure 11. Spatial view of the archived distance-weighted evaluation.*

[Open the spatial evaluation map](Figures/04_distance_weighted_tversky_map.png)

### 6.4 Feature signatures

![Model feature signatures](Figures/08_model_feature_signatures.png)

*Figure 12. Feature-signature diagnostics for interpreting model behavior.*

[Open the feature-signatures figure](Figures/08_model_feature_signatures.png)

Feature importance indicates how the fitted model uses predictors under a particular dataset and model specification. It does not establish causal geological importance.

---

## 7. Data and results

The `Tables/` directory contains the archived CSV artifacts described in the report.

### 7.1 Summary tables

| File                                                                                  | Description                                                |
| ------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [GEMS_portfolio_summary.csv](Tables/GEMS_portfolio_summary.csv)                       | Archived project configuration and portfolio-level metrics |
| [prediction_summary.csv](Tables/prediction_summary.csv)                               | Prediction coverage, range, and raster summary statistics  |
| [model_performance.csv](Tables/model_performance.csv)                                 | Model performance and threshold-related diagnostics        |
| [distance_weighted_tversky_summary.csv](Tables/distance_weighted_tversky_summary.csv) | Separate weighted-contribution evaluation summary          |

### 7.2 Feature and input inventories

| File                                                        | Description                         |
| ----------------------------------------------------------- | ----------------------------------- |
| [feature_statistics.csv](Tables/feature_statistics.csv)     | Feature-level statistical summaries |
| [selected_input_files.csv](Tables/selected_input_files.csv) | Selected input-file inventory       |

### 7.3 Prediction and threshold analysis

| File                                                                          | Description                                   |
| ----------------------------------------------------------------------------- | --------------------------------------------- |
| [prospectivity_cells.csv](Tables/prospectivity_cells.csv)                     | Archived prospectivity cell records           |
| [top_100_prospectivity_targets.csv](Tables/top_100_prospectivity_targets.csv) | Ranked high-prospectivity target records      |
| [threshold_analysis.csv](Tables/threshold_analysis.csv)                       | Threshold sensitivity results                 |
| [dwt_pixel_contributions.csv](Tables/dwt_pixel_contributions.csv)             | Pixel-level weighted evaluation contributions |

Browse the complete [Figures directory](Figures/) and [Tables directory](Tables/).

The available file inventory documents the presence of these artifacts; it does not by itself establish independent validation, complete data provenance, or official competition acceptance.

---

## 8. Methodology

The workflow consists of six conceptual stages.

### Stage 1 — Data preparation

* Inventory available rasters and tabular files.
* Check CRS, dimensions, transforms, bounds, units, and NoData masks.
* Align compatible data sources to a common grid.
* Document resampling and interpolation choices.
* Preserve missing coverage rather than silently replacing it with zero.

### Stage 2 — Feature construction

* Assemble base geophysical predictors.
* Include terrain and contextual predictors where supported by the source data.
* Derive local gradients and neighborhood features where justified.
* Examine correlated predictors and sensitivity to noise.
* Maintain a traceable feature inventory.

### Stage 3 — Model fitting

The archived portfolio uses LightGBM, a gradient-boosted decision-tree model capable of learning nonlinear relationships among heterogeneous predictors.

The model learns statistical associations with the available training labels. It does not inherently encode geological causation, structural topology, or fault continuity.

### Stage 4 — Evaluation

The archived report records:

* ROC-AUC;
* precision–recall AUC;
* distance-weighted Tversky diagnostics;
* threshold analysis;
* weighted true-positive, false-positive, and false-negative contributions.

Spatially blocked validation is recommended to assess transfer to geographically distinct regions. The summary values alone do not establish that the archived folds were geographically independent or that all threshold tuning was nested correctly.

### Stage 5 — Prediction mapping

The reported output grid has:

* Width: 3,292 cells;
* Height: 3,730 cells;
* Nominal resolution: 100 m;
* CRS: EPSG:32611;
* Finite prediction cells: 4,733,111.

These values describe the archived output. Before formal submission, the actual raster must be checked for dimensions, transform, bounds, CRS, data type, NoData representation, and permitted score range.

### Stage 6 — Geological review

High-ranking candidates should be assessed for:

* spatial continuity and orientation;
* agreement among independent geophysical products;
* geomorphic plausibility;
* relation to known geological structures;
* alternative explanations, including lithological boundaries and drainage;
* stability across validation folds, model configurations, and data perturbations.

The output is a ranking surface to guide review, not an autonomous declaration of newly discovered faults.

---

## 9. Distance-weighted Tversky evaluation

The conventional Tversky index is

$$
T_{\alpha,\beta}
=
\frac{TP}{TP+\alpha FP+\beta FN},
$$

where \(TP\), \(FP\), and \(FN\) represent true-positive, false-positive, and false-negative contributions.

The archived portfolio reports a 300 m tolerance, equivalent to three nominal 100 m pixels, with \(\alpha=0.2\) and \(\beta=0.8\).

The distance-weighted implementation modifies the contributions according to spatial proximity. Official comparisons must use the exact competition scoring implementation rather than a substitute approximation.

### Archived weighted-contribution summary

| Quantity                           | Recorded value |
| ---------------------------------- | -------------: |
| Weighted true positives, \(TP_w\)  |      26,283.97 |
| Weighted false positives, \(FP_w\) |     255,000.52 |
| Weighted false negatives, \(FN_w\) |      34,704.00 |
| \(\alpha\)                         |            0.2 |
| \(\beta\)                          |            0.8 |
| Distance tolerance                 |          300 m |
| Nominal tolerance                  |       3 pixels |
| Separate recorded DWT              |         0.2502 |

Source: [distance_weighted_tversky_summary.csv](Tables/distance_weighted_tversky_summary.csv).

### Why multiple DWT values appear

The portfolio records a mean probabilistic DWT of 0.0616, a mean best hard DWT of 0.1148, and a separate DWT summary of 0.2502.

These values must remain separate because they may reflect different prediction sets, aggregation methods, thresholds, or evaluation contexts. The generating notebook and scoring implementation must be checked before these scores are compared or reported as official results.

Distance weighting can reward spatially close predictions, but broad predictions can still produce a substantial false-positive burden. The practical objective is to improve useful spatial agreement without overwhelming geological review with implausible candidates.

---

## 10. Reproducibility and validation

A reproducible mapping workflow should preserve enough information to regenerate the predictions and understand the source of every reported metric.

### Validation checklist

* [ ] Preserve the original input-file inventory.
* [ ] Record software versions, random seeds, and model parameters.
* [ ] Document feature definitions, units, provenance, and effective source resolution.
* [ ] Save spatial fold geometries and held-out regions.
* [ ] Fit preprocessing and feature selection using training data only within each fold.
* [ ] Select thresholds without using held-out evaluation labels.
* [ ] Test the official distance-weighted metric against controlled examples.
* [ ] Record per-fold metrics and positive-label prevalence.
* [ ] Compare geophysics-only, terrain-only, and combined feature sets.
* [ ] Validate raster CRS, transform, dimensions, NoData, and score range.
* [ ] Associate each metric with the exact evaluated prediction set.
* [ ] Preserve model and artifact versions where permitted.

### Recommended experiments

| Experiment                    | Research question                                                       |
| ----------------------------- | ----------------------------------------------------------------------- |
| Geophysics-only baseline      | How much predictive value comes from the base geophysical bands?        |
| Terrain-only model            | How useful are terrain-derived features by themselves?                  |
| Combined model                | Does evidence integration improve the ranking?                          |
| Derived-feature ablation      | Do gradients and contextual features provide incremental value?         |
| Spatially blocked validation  | Does the model generalize to geographically distinct areas?             |
| Threshold sensitivity         | How does the false-positive burden change with recall?                  |
| Model ensemble                | Are the highest-ranked targets stable across model variations?          |
| Independent geological review | Do candidate targets have plausible support beyond the training labels? |

These are recommended next steps, not assertions that all experiments have already been completed.

---

## 11. Repository structure

The repository uses `Figures/` and `Tables/` as the primary directories for visual and tabular artifacts.

```text
GeologicEnhancedMap/
├── README.md
├── Figures/
│   ├── .gitkeep
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
│   └── 08_model_feature_signatures.png
└── Tables/
    ├── .gitkeep
    ├── GEMS_portfolio_summary.csv
    ├── distance_weighted_tversky_summary.csv
    ├── dwt_pixel_contributions.csv
    ├── feature_statistics.csv
    ├── model_performance.csv
    ├── prediction_summary.csv
    ├── prospectivity_cells.csv
    ├── selected_input_files.csv
    ├── threshold_analysis.csv
    └── top_100_prospectivity_targets.csv
```

This listing reflects the repository inventory supplied for the project. Add notebooks, model files, raster outputs, or other directories to this tree only after confirming that they are present in the repository.

---

## 12. Research roadmap

### Priority 1 — Audit the evaluation pipeline

Verify the official scoring implementation, reconcile the separate DWT summaries, and document the exact predictions, thresholds, folds, and aggregation methods used for each result.

### Priority 2 — Strengthen spatial validation

Use geographically separated folds or structurally distinct regions. Record fold boundaries, label prevalence, and per-region metrics.

### Priority 3 — Measure feature-family contributions

Run controlled ablations to determine whether terrain, geophysical derivatives, and contextual features improve results beyond the base geophysical model.

### Priority 4 — Improve spatial coherence

Investigate candidate continuity, orientation, and structural intersections while controlling the false-positive burden.

### Priority 5 — Quantify uncertainty

Compare fold-level predictions, alternative model configurations, and input perturbations. Identify stable candidates separately from those whose ranking is sensitive to modeling choices.

### Priority 6 — Independently assess high-ranking targets

Compare candidates against independent geological maps, source geophysical products, imagery, and field evidence where available.

The goal is not simply to increase a single metric. It is to produce a more reliable, interpretable, and scientifically defensible set of candidate structures.

---

## 13. Limitations

**Incomplete labels:** An unlabeled pixel may contain an unmapped fault rather than a true negative.

**Spatial dependence:** Nearby pixels and spatially smooth raster features are correlated. Random pixel splits can overstate generalization.

**Coverage gaps:** Approximately 38.55% of the recorded output grid contains finite predictions. Uncovered cells must remain distinguishable from low-scoring cells.

**Resolution mismatch:** A nominal 100 m output grid does not imply that every input source has 100 m effective resolution.

**Lineament ambiguity:** Roads, drainage, erosional features, lithological boundaries, and processing artifacts may resemble geological structures.

**Model interpretation:** Feature importance describes model behavior, not causal geological control.

**Metric consistency:** Scores from different folds, thresholds, prediction sets, or aggregation procedures must not be treated as interchangeable.

**Geothermal uncertainty:** A potential fault does not establish temperature, fluid availability, permeability, sustainable production, or economic viability.

The intended role of GEMS is to prioritize further investigation while preserving uncertainty and the need for independent verification.

---

## 14. References

1. Ahmadi, H., and Pekkan, E. (2021). Fault-based geological lineaments extraction using remote sensing and GIS—a review. *Geosciences*, 11(5), 183. https://doi.org/10.3390/geosciences11050183

2. Faulds, J. E., Hinz, N. H., Coolbaugh, M. F., et al. (2021). Geological controls on geothermal resources for power generation. *Nature Reviews Earth & Environment*, 2, 324–339. https://doi.org/10.1038/s43017-021-00154-y

3. van der Meer, F. D., Hecker, C. A., van Ruitenbeek, F. J., et al. (2014). Geologic remote sensing for geothermal exploration: A review. *International Journal of Applied Earth Observation and Geoinformation*, 33, 255–269. https://doi.org/10.1016/j.jag.2014.05.007

4. U.S. Department of Energy, Geothermal Technologies Office. (2026). Office of Geothermal Announces Geologic Enhanced Mapping System (GEMS) Prize. [Official announcement](https://www.energy.gov/hgeo/geothermal/articles/office-geothermal-announces-geologic-enhanced-mapping-system-gems-prize).

These references provide scientific context. They do not independently validate the model outputs or archived metrics in this repository.

---

## 15. Acknowledgements

This independent research portfolio is framed around the Geologic Enhanced Mapping System (GEMS) Prize announced by the U.S. Department of Energy.

**Author:** Umar Tabbsum
**Role:** Independent Researcher
**Research areas:** Geospatial machine learning, geological fault mapping, and geothermal exploration
**Report date:** October 2026

This project should not be represented as endorsed by the U.S. Department of Energy, the National Lab of the Rockies, or DrivenData.

---

## Final perspective

GEMS investigates how heterogeneous geophysical evidence, terrain context, and machine learning can be combined to prioritize geological structures that merit closer examination.

Its contribution should ultimately be judged by the reproducibility of the workflow, the rigor of its spatial validation, the transparency of its uncertainty, and the independent geological defensibility of its candidate targets.

**Mapping evidence. Ranking possibilities. Supporting discovery.**
