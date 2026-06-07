# Spatial Inequities in the Degradation of Night Sky Visibility
### Globe at Night × UNDP HDI — Full Analysis Pipeline

---

# IMPORTANT:
## This project was designed, structured, and written by myself. However, **I also used an AI assistant was used to clean up code formatting, fix typos, organize documentation cells, standardize data dictionaries, and make the charts look clean and professional**

---

## Project Overview
This repository holds a Python notebook that looks at how human development impacts the environment. Specifically, it studies how global light pollution cuts down our view of the night sky. 

**Main Question:** How does the average brightness of a country's night sky relate to its Human Development Index (HDI), and is this relationship a straight line or a curve?

The project answers this by combining citizen-science night sky data from the **Globe at Night** project (2006–2024) with the United Nations Development Programme (**UNDP**) Human Development Index. It checks if light pollution grows steadily with development, or if it follows a more complicated, non-linear path.

---

## Data Dictionary

| Variable / Term | What It Means |
| :--- | :--- |
| **LimitingMag** | Limiting magnitude is a measure of how faint a star you can see with your naked eye. A higher number means a darker sky with less light pollution. The scale goes from 1 (very bright sky; you can only see the moon or bright planets) to about 7 (a perfectly dark, natural sky). |
| **HDI (Value)** | The UN Human Development Index scores countries from 0 to 1 based on life expectancy, education, and income. A higher number means a higher level of development. |
| **valid_data_points** | The number of clean citizen-science observations recorded for a country. This only counts observations with a valid sky brightness rating between 1 and 7. It helps show how reliable a country's average score is. |

---

## Notebook Structure

The analysis runs step-by-step through a single Jupyter notebook (`Updated_Results.ipynb`), divided into ten parts:

1. **Setup & Imports:** Loads the necessary Python tools for data handling, graphing, and statistics (like `scipy.stats`, `statsmodels`, `scikit-learn`, and `optuna`).
2. **Data Loading & Cleaning:** * Combines yearly files from the Globe at Night database (2006–2024).
   * Standardizes country names so the datasets match up perfectly.
   * Removes small territories that do not have an official UN HDI score.
3. **Initial Charts:** Uses smooth trend lines and bubble plots to get a first look at the data without forcing it into a specific mathematical shape.
4. **Baseline Models:** Tests standard straight-line and logarithmic models to see if the relationship is linear.
5. **Testing for Curves (Core Analysis):**
   * Fits a curved (quadratic) line to the data and checks if it is statistically meaningful.
   * Calculates the exact peak point to find where night skies are the clearest.
   * Runs the same test on a filtered group of countries with at least 30 observations to make sure small sample sizes aren't ruining the results.
   * Splits the data into segments and groups to double-check the direction of the trend.
6. **Advanced Machine Learning:** Tests advanced models like Random Forest and Gradient Boosting, using an optimizer called Optuna to find the best settings.
7. **Comparing Models:** Ranks all models side-by-side using accuracy metrics to see which one predicts sky clarity best.
8. **Error Checks (Diagnostics):** Evaluates the main curved model to ensure the errors are distributed normally and don't show hidden biases.
9. **Country Breakdown:** Identifies and charts the top 20 darkest and top 20 brightest countries, using data filters to keep it accurate.
10. **Final Summary:** Gathers all the key statistics and prints out clear conclusions.

---

## Key Findings

* **Straight Lines Don't Work:** Standard correlation tests show almost zero relationship. This happens because the true trend is a curve that goes up and then down. A straight-line test gets confused by this shape and mathematically cancels the trend out.
* **The Inverted-U Shape:** The curved model proves that night sky visibility starts out low in developing nations, reaches its clearest point in medium-developed nations (HDI around 0.650 to 0.700), and then drops sharply as countries become highly developed.
* **HDI Doesn't Explain Everything:** Even though the curved trend is real and statistically significant, the overall models have low predictive power ($R^2$). This means HDI alone cannot predict light pollution. Local issues like city layout, population density, and local energy laws matter much more.

---

## Requirements

To run this notebook, you will need to install these Python packages:

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn statsmodels openpyxl optuna
