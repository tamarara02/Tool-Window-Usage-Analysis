# JetBrains IDE Tool Window Usage Analysis

This project analyzes **tool window usage in JetBrains IDEs** to understand how long tool windows remain open depending on how they were opened — **manually by the user** or **automatically by the IDE**.  

The goal is to identify usage patterns, quantify differences in session durations, and assess whether the method of opening affects user behavior. The analysis includes both **descriptive statistics** and **statistical testing**, accompanied by **visualizations** to illustrate the differences.

By combining numerical and visual analysis, this project helps answer questions such as:  
- Do users close manually opened tool windows faster than automatically opened ones?  
- Are the differences in duration statistically significant?  
- What is the typical magnitude of the difference between manual and automatic sessions?  

The results can be useful for IDE developers and UX researchers to optimize tool window behavior and improve the user experience.

---

## 1. Files Required

Ensure the following files are in the same folder:

- `project.ipynb` → The main Jupyter Notebook containing the full analysis.  
- `toolwindow_data.csv` → Dataset containing tool window events, including open/close timestamps and open type.

---

## 2. Installation

You need **Python 3** installed on your system.  

Install the required libraries using pip:

```bash
pip install pandas numpy matplotlib scipy notebook
```
This will install all dependencies required to run the notebook

---

## 3. How to Run the Notebook

1. Open a terminal or Command Prompt in the folder containing the project files.  
2. Launch Jupyter Notebook:

```bash
jupyter notebook
```

3. Open project.ipynb in the browser.

4. In the menu, select Kernel → Restart & Run All to execute all cells.

This will run the full analysis and generate all descriptive statistics, visualizations, and statistical tests.

---

## 4. Analysis Overview

The analysis workflow includes:

1. **Data Cleaning and Session Reconstruction**  
   - Remove orphan close events and unmatched opens.  
   - Match each open with the next close to reconstruct full sessions.  
   - Label each session as `manual` or `auto`.

2. **Descriptive Statistics**  
   - Compute mean, median, standard deviation, and quartiles for manual and automatic sessions.  
   - Identify skewness caused by extreme values.

3. **Visualization**  
   - **Histograms (log-transformed)** to show the overall distribution of session durations.  
   - **Boxplots and violin plots** to highlight differences between manual and automatic sessions.  
   - **CDF plots** to illustrate the cumulative probability distribution of durations.

4. **Statistical Testing**  
   - **Mann-Whitney U Test** (non-parametric) for distribution comparison.  
   - **Hodges–Lehmann Estimator** with bootstrap confidence interval for median shift.  
   - **Welch’s t-test** applied to log-transformed durations to validate differences under approximate normality.  
   - **Effect size** measured via rank-biserial correlation.

---

## 5. Notes

- The CSV file must be in the same folder as the notebook.  
- Ensure all cells are run for complete results and graphs.  
- Log transformation is used only for Welch's t-test to reduce the influence of extreme outliers.  
- Bootstrap confidence intervals (Hodges–Lehmann estimator) may take around a minute to compute — please wait until it finishes.
- Results are reproducible if the notebook is run in order.

---

## 6. Author & Project Info

**Author:** Tamara Radojčić  
**Date:** October 2025  
**Project:** JetBrains Analytics for Data Products IDEs  

**Key Insights:**

- Manual sessions are typically shorter, with many closing quickly.  
- Automatic sessions generally stay open longer, with fewer but very long sessions.  
- Statistical tests confirm that the difference between manual and automatic sessions is **significant and practically relevant**.  
- The Hodges–Lehmann estimator gives a robust estimate of the typical median difference.  
- Visualizations help intuitively compare distributions and identify patterns in user behavior.

