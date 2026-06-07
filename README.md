import json

# Define the README content
readme_text = """# Spatial Inequities in the Degradation of Night Sky Visibility
### Globe at Night × UNDP HDI — Full Analysis Pipeline

---

### IMPORTANT DEVELOPMENT DISCLAIMER
This research pipeline was initially designed, structured, and written via human-driven coding. Following the initial core development, an AI assistant was utilized exclusively to clean up code syntax, reformat documentation cells, standardize data harmonization dictionaries, and apply professional styling to the statistical visualizations. The underlying methodology, research design, and interpretive logic remain completely human-conceived.

---

## Research Overview
This repository contains a comprehensive analytical notebook that investigates the global relationship between human development and environmental degradation—specifically, the loss of the night sky due to artificial light pollution. 

**Core Research Question:** How does average naked-eye night sky visibility (limiting magnitude) relate to a country's Human Development Index (HDI), and is that relationship linear or nonlinear?

By cross-referencing citizen-science night sky observations from the **Globe at Night** project (2006–2024) with the United Nations Development Programme (**UNDP**) Human Development Index, this analysis explores whether spatial inequities in light pollution follow a monotonic trend or a complex, non-linear trajectory.

---

## Data Dictionary

| Variable / Term | Definition |
| :--- | :--- |
| **LimitingMag** | The limiting magnitude represents the faintest star visible to the naked eye under current local sky conditions. A higher value denotes a darker, less light-polluted sky. The scale ranges from 1 (only the Moon or brightest planets are visible) to approximately 7 (pristine, natural dark sky). |
| **HDI (Value)** | The UN Human Development Index is a composite statistic measuring average achievement in three basic dimensions of human development: a long and healthy life, knowledge, and a decent standard of living. Scale ranges from 0 to 1 (higher equals greater development). |
| **valid_data_points** | The total count of raw citizen-science observations for a specific country that passed strict quality filtering (limiting magnitude strictly within the range of 1 to 7). This metric serves as a reliability indicator for country-level averages. |

---

## Technical Architecture & Notebook Structure

The analysis is executed sequentially through a single Jupyter notebook (`Updated_Results.ipynb`), divided into ten distinct structural phases:

1. **Setup & Imports:** Standardizes the environment by importing specialized statistical, machine learning, and optimization packages (`scipy.stats`, `statsmodels`, `scikit-learn`, `optuna`).
2. **Data Loading & Preprocessing:** * Compiles annual multi-year CSV files from the Globe at Night database (2006–2024).
   * Standardizes and harmonizes cross-dataset country nomenclatures (e.g., mapping historical or stylistic naming variances to match official UNDP records).
   * Filters out geographical territories lacking dedicated HDI evaluations to remove analytical noise.
3. **Exploratory Visualizations:** Uses LOWESS smoothing on raw observations and log-scaled bubble scatterplots to evaluate initial trends without imposing strict functional forms.
4. **Baseline Regression:** Establishes standard benchmark models assuming monotonic structures, including Pearson/Spearman correlation matrices, ordinary linear regression, and logarithmic functions.
5. **Nonlinearity Investigation (Core Novel Analysis):**
   * Fits a quadratic regression model and conducts a formal F-test on the quadratic term.
   * Calculates the exact turning/peak point mathematically to locate maximum sky visibility.
   * Replicates the workflow on a sample-size-filtered subset ($\ge 30$ valid data points) to prevent small-sample anomalies from warping results.
   * Conducts piecewise linear segmentations and an HDI tertile-split ANOVA direction test.
6. **Advanced Predictive Modeling:** Implements higher-degree polynomial cross-validation, alongside Random Forest and Gradient Boosting architectures fine-tuned via Optuna hyperparameter optimization.
7. **Model Comparison:** Ranks all linear, non-linear, and ensemble models side-by-side using Cross-Validated $R^2$ and Cross-Validated Root Mean Squared Error (RMSE).
8. **Residual Diagnostics:** Evaluates the primary quadratic OLS model using residual-versus-fitted plots, histogram frequencies, and a Shapiro-Wilk normality assessment.
9. **Country-Level Visualizations:** Visualizes the top 20 darkest and top 20 most light-polluted nations using sample-size filters, alongside quartile box plots.
10. **Final Results Summary:** Consolidates the statistical findings and presents programmatic conclusions.

---

## Key Statistical Findings

* **The Fallacy of Linear Metrics:** Traditional linear correlation tests (Pearson and Spearman) yield near-zero coefficients. This occurs because the true relationship is non-linear; the positive left half and the negative right half of the distribution mathematically cancel each other out in linear equations.
* **The Inverted-U Trajectory:** The quadratic model uncovers a highly significant inverted-U curve ($p$-value is statistically robust under the F-test). Night sky visibility is low in least-developed nations, reaches a peak around a medium HDI tier ($\approx 0.650–0.700$), and subsequently degrades severely as countries cross into high and very high development brackets.
* **Low Predictive Variance ($R^2$):** Cross-validated models show low overall $R^2$ scores across the board. This indicates that while the non-linear trend is statistically real, HDI alone is not a sufficient predictor of light pollution. Factors such as localized population density, urban grid design, and regional energy policies account for the vast remainder of variance.

---

## Requirements & Environment

To run this pipeline, ensure your Python environment has the following dependencies installed:
