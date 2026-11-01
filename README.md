# Exploratory Data Analysis on the KosteckiDillon Migraine Dataset

**Course:** BCSE331L — Exploratory Data Analysis  
**Semester:** Fall Semester 2026–27  
**Name:** Chunduri Sai Kaushik  
**Register Number:** 23BDS0339

---

## 📌 Submission Links

| Item | Link |
|---|---|
| GitHub Repository | [Exploratory-Data-Analysis](https://github.com/Kaushik-verse/Exploratory-Data-Analysis) |
| Video Demonstration | [Google Drive](https://drive.google.com/drive/folders/1yFpv91-KLxvb4fRh7OU_qf-qMEBTj15Q?usp=sharing) |

> Both links are set to **public / anyone with the link can view**.

---

## 📖 About This Project

This project performs a **comprehensive Exploratory Data Analysis (EDA)** on the **KosteckiDillon** dataset — a longitudinal clinical study of **133 migraine patients** who kept daily headache diaries around the time they started a biofeedback treatment programme.

Each row in the dataset represents **one patient on one day** (4,152 patient-days total), with 10 variables capturing patient demographics, headache occurrence, medication status, air quality, and temporal information.

### Guiding Question

> **What distinguishes a patient-day on which a migraine occurs from one on which it does not, and can those differences be summarised, visualised and modelled?**

### Dataset Source

```
https://raw.githubusercontent.com/salemprakash/EDA/main/Data/KosteckiDillon.csv
```

---

## 📊 Dataset Description

| Column | Meaning | Type | Measurement Scale |
|---|---|---|---|
| `rownames` | Original row index | Numerical, discrete | Nominal (ID only) |
| `id` | Patient identifier (1–133) | Numerical, discrete | Nominal |
| `time` | Days relative to treatment start (negative = before, positive = after) | Numerical, discrete | Interval |
| `dos` | Day of study (sequential day number) | Numerical, discrete | Interval |
| `hatype` | Headache type: Aura / No Aura / Mixed | Categorical | Nominal |
| `age` | Patient age in years | Numerical, continuous | Ratio |
| `airq` | Air quality index on that day | Numerical, continuous | Ratio |
| `medication` | Medication status: continuing / reduced / none | Categorical | Ordinal |
| `headache` | Did a headache occur? yes / no | Categorical, binary | Nominal |
| `sex` | female / male | Categorical, binary | Nominal |

**Key structural feature:** The `time` variable runs from negative to positive around the treatment start, enabling **before vs. after treatment comparisons** for the same patient.

---

## 🗂️ Module Coverage Map

The project covers **Modules 2–7** of the BCSE331L syllabus in a logical, analyst-driven order:

| Module | Topic | Notebook Section |
|---|---|---|
| **Module 2** | Data Transformation | Section 4 |
| **Module 3** | Correlation Analysis & Time Series Analysis | Section 5 |
| **Module 4** | Data Summarization & Visualization | Section 6 |
| **Module 5** | Clustering Algorithms | Section 7 |
| **Module 6** | Dimensionality Reduction | Section 8 |
| **Module 7** | Model Development & Evaluation (incl. Reinforcement Learning) | Section 9 |
| — | Observations, Inference & Conclusion | Section 10 |

---

## 🔬 Features & Techniques Used

### Section 4 — Data Transformation (Module 2)

- **4.1 Data Deduplication**
  - Fully identical row detection (ignoring `rownames`)
  - Logical duplicate detection on `(id, time)` patient-day keys
  - Removal of 1 genuine duplicate row found

- **4.2 Replacing Values**
  - Dropping the meaningless `rownames` index column
  - Normalising categorical text (lowercased, stripped)
  - Binary encoding of `headache` (yes/no → 1/0) and `sex` (female/male → 1/0)
  - Ordinal encoding of `medication` (none < reduced < continuing)
  - One-hot encoding of `hatype` (nominal, no false ordering)
  - Derived `post_treatment` flag from the `time` variable

- **4.3 Discretization and Binning**
  - Equal-width binning of air quality
  - Equal-frequency (quantile) binning of air quality
  - Domain-driven binning of age into clinical groups

- **4.4 Missing Data — Introduction**
  - Controlled experiment: artificially injecting MCAR missingness into a complete dataset
  - Missingness heatmap visualization

- **4.5 Traditional Imputation Methods**
  - Listwise deletion (complete-case analysis)
  - Mean imputation
  - Median imputation
  - Forward fill within each patient (exploiting longitudinal structure)

- **4.6 Maximum Likelihood Estimation (MLE) for Missing Data**
  - Iterative Imputer (EM / MICE-style) using scikit-learn
  - Hand-coded EM algorithm for bivariate normal (transparent, not a black box)

- **4.7 Scoring Imputation Methods Against Ground Truth**
  - RMSE comparison across all methods
  - Variance preservation analysis
  - Correlation preservation analysis
  - Distribution shape comparison (KDE overlays)

### Section 5 — Correlation Analysis & Time Series (Module 3)

- **5.1 Univariate Analysis**
  - Histograms, KDE plots, and box plots for all numerical variables
  - Count plots and frequency tables for all categorical variables

- **5.2 Bivariate Analysis**
  - Pearson and Spearman correlation matrices with heatmaps
  - Point-biserial correlation of numeric variables with headache outcome
  - Independent-samples t-tests (headache days vs. non-headache days)
  - One-way ANOVA across headache types
  - Chi-square tests of independence for all categorical pairs
  - Cramér's V effect size measures
  - Standardised residual analysis for contingency tables
  - Headache proportion plots by category

- **5.3 Multivariate Analysis**
  - Pair plots coloured by outcome
  - Three-way interaction: medication effect by headache type
  - Four-way view: age group × medication, split by sex
  - VIF (Variance Inflation Factor) for multicollinearity check

- **5.4 Time Series Fundamentals**
  - Time-based indexing using `dos` as a datetime proxy
  - Pre vs. post treatment comparison at the patient level (paired t-test)

- **5.5 Time Series Visualization**
  - Headache rate over calendar time with rolling mean (7-day window)
  - Air quality time series
  - Patient coverage over time (reporting density)
  - Treatment-relative timeline analysis

- **5.6 Grouping Time Series Data**
  - Day-of-week aggregation and headache rate analysis
  - Monthly aggregation
  - Medication-stratified time series
  - Chi-square test for weekly pattern significance

- **5.7 Resampling Time Series**
  - Weekly and monthly resampling with aggregation

### Section 6 — Data Summarization & Visualization (Module 4)

- **6.1 Statistical Summary Measures**
  - Central tendency (mean, median, mode)
  - Dispersion (variance, standard deviation, IQR, range, coefficient of variation)
  - Shape (skewness, kurtosis)

- **6.2 Data Elaboration**
  - Derived features from patient-level aggregation (headache rate, longest streak, mean air quality, etc.)

- **6.3 1-D Statistical Data Analysis**
  - Comprehensive univariate profiling with distribution plots

- **6.4 2-D Statistical Data Analysis & Contingency Tables**
  - Cross-tabulations with row/column percentages
  - Chi-square tests with standardised residuals
  - Mosaic-style proportion visualizations

- **6.5 n-D Statistical Data Analysis**
  - Multi-way grouped summaries
  - Faceted visualizations across 3–4 variables simultaneously

- **6.6–6.8 Visualization Techniques**
  - Scatter plots, dot charts, and bar plots
  - All with consistent styling and interpretive annotations

### Section 7 — Clustering Algorithms (Module 5)

- **7.1 Spectral Clustering**
  - RBF kernel affinity matrix
  - Silhouette score evaluation across K = 2–8

- **7.2 Minimum Spanning Tree (MST) Clustering**
  - MST construction and edge-length distribution analysis
  - Demonstration of degenerate clustering (131/1/1) due to continuous edge distribution

- **7.3 Model-Based Clustering (GMM + EM)**
  - Gaussian Mixture Models with BIC/AIC model selection
  - Soft assignment analysis (posterior probabilities)
  - Only 1.5% of patients have ambiguous assignments (< 0.8 probability)

- **7.4 Hierarchical Agglomerative Clustering**
  - Ward, complete, and average linkage dendrograms
  - Cluster profiling: identification of a high-burden subgroup (45 patients, 91% headache rate, 19.7-day mean streak)

- **7.5 Outlier Detection Using Clustering**
  - Multi-method consensus outlier detection
  - Validation that outliers are genuine clinical extremes (long diaries, 63–121 days), not artefacts
  - Adjusted Rand Index (ARI) comparison across all clustering methods

### Section 8 — Dimensionality Reduction (Module 6)

- **8.1 Principal Component Analysis (PCA)**
  - Scree plot and eigenvalue analysis with Kaiser criterion
  - Loadings heatmap and biplot visualization
  - 5 components needed for 90% variance; PC1 = severity (27.1%)

- **8.2 Singular Value Decomposition (SVD)**
  - Full SVD decomposition and PCA equivalence verification
  - Low-rank matrix reconstruction at varying ranks
  - TruncatedSVD via scikit-learn

- **8.3 Factor Analysis**
  - Bartlett's test of sphericity
  - Factor analysis across multiple factor counts with BIC selection
  - Uniqueness analysis: age has 98.6% unique variance
  - Factor 1 = severity, Factor 2 = air-quality exposure

- **8.4 Intrinsic Dimensionality Estimation**
  - PCA variance thresholds
  - Participation ratio
  - Levina-Bickel MLE estimator
  - Intrinsic dimensionality ≈ 5 out of 7 features

- **8.5 Multidimensional Scaling (MDS)**
  - Metric MDS (preserves actual distances)
  - Non-metric MDS (preserves rank order of distances)
  - Shepard diagram for distance fidelity
  - Stress analysis across increasing dimensions

- **8.6 Manifold Learning**
  - Isomap (geodesic distances)
  - Locally Linear Embedding (LLE) — standard and modified
  - Geodesic vs. Euclidean distance comparison
  - kNN neighbourhood preservation scoring

- **8.7 Self-Organizing Maps (SOM)**
  - Custom SOM implementation
  - Convergence monitoring
  - Hit map, U-matrix, and component plane visualizations

### Section 9 — Model Development & Evaluation (Module 7)

- **9.1 Linear Regression**
  - Patient-level regression (headache rate prediction)
  - StandardScaler preprocessing
  - Train/test split with cross-validation (5-fold)
  - Baseline comparison (predicting the mean)
  - Diagnostic plots: predicted vs. actual, residuals vs. fitted, residual distribution, coefficient importance
  - Result: Training R² = 0.147, Test R² = **-0.183** (worse than baseline — no signal)

- **9.2 Logistic Regression**
  - Daily-level classification (headache yes/no)
  - Majority-class baseline comparison (0.643 accuracy)
  - Confusion matrix, ROC curve, AUC analysis
  - Result: Accuracy 0.660 (only +1.7pp above baseline), AUC = 0.632
  - Threshold sensitivity analysis (precision-recall trade-off)
  - Balanced accuracy: 0.530 (near coin-flip)

- **9.3 Reinforcement Learning**
  - Conceptual comparison: supervised vs. reinforcement learning
  - Explanation of why this dataset cannot support true RL
  - Multi-Armed Bandit simulation using observed medication reward distributions
  - Strategies implemented: Pure Greedy, Epsilon-Greedy, UCB (Upper Confidence Bound)
  - Cumulative reward, cumulative regret, arm selection frequency, exploration rate plots
  - Multi-seed Monte Carlo analysis (30 seeds) to avoid single-run misleading conclusions

### Section 10 — Observations, Inference & Conclusion

- Detailed module-by-module observations with corrections to initial expectations
- Integrated inference across all modules
- Key finding: **between-patient variation dominates; within-patient day-to-day variation is unexplained by this feature set**
- Recommendation: mixed-effects logistic model with per-patient random intercepts
- Negative results reported as valuable findings (air quality null, no treatment effect, no natural clusters, models worse than baselines)

---

## 🔑 Key Findings

1. **Air quality does NOT predict headache occurrence** (r = 0.0145, p = 0.35) — a clean null result for a widely-held belief
2. **Medication status is the strongest categorical signal** (Cramér's V = 0.229) but the relationship is **non-monotone** — the *reduced* group has the highest headache rate (77.5%), not the *continuing* group
3. **No measurable treatment effect** — before vs. after headache rates are 0.652 and 0.648 (paired t-test p = 0.897)
4. **No natural clusters** exist — patients vary along a smooth continuum; silhouette scores are flat across K = 2–8
5. **One genuinely distinct severe subgroup** — 45 patients with 91% headache rate and 19.7-day mean unbroken streaks
6. **Features are nearly independent** — intrinsic dimensionality ≈ 5 out of 7; age has 98.6% unique variance
7. **Both predictive models fail** — linear regression R² = -0.183 (test), logistic accuracy only +1.7pp above majority-class baseline
8. **Structure is linear, not manifold** — MDS outperforms Isomap and LLE on both global and local metrics

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| **NumPy** | Numerical computation |
| **pandas** | Data manipulation and analysis |
| **Matplotlib** | Base plotting library |
| **Seaborn** | Statistical data visualization |
| **SciPy** | Statistical tests, distance computation, hierarchical clustering, MST |
| **scikit-learn** | Preprocessing, clustering, dimensionality reduction, regression, classification, imputation, evaluation metrics |

---

## 🚀 How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Kaushik-verse/Exploratory-Data-Analysis.git
   cd Exploratory-Data-Analysis
   ```

2. **Install dependencies:**
   ```bash
   pip install numpy pandas matplotlib seaborn scipy scikit-learn
   ```

3. **Open and run the notebook:**
   ```bash
   jupyter notebook EDA_Project_23BDS0339.ipynb
   ```
   
   The notebook loads data directly from a remote URL. If run offline, place `KosteckiDillon.csv` in the same directory — the notebook has a built-in fallback.

4. **Reproducibility:** A fixed random seed (`RANDOM_STATE = 42`) ensures all stochastic methods (GMM, spectral clustering, SOM, train/test splitting) produce identical results on every run.

---

## 📁 Project Structure

```
Exploratory-Data-Analysis/
├── EDA_Project_23BDS0339.ipynb   # Complete analysis notebook (all Modules 2–7)
├── README.md                      # This file
```

---

## 📝 License

This project is submitted as part of the BCSE331L coursework at VIT.
